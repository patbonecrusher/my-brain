---
creation date: 2023-12-21 22:33
modification date: Thursday, 21st December 2023, 22:33:26
tags:
  - today_i_leaned
  - computer/language
  - computer/language/cpp
---

## The C++ 11 way

``` c++
#include <stdio.h>
#include <stdlib.h>
#include <functional>

  

typedef int nm_event_t;

class A {
public:
	typedef void (*event_callback_t)(nm_event_t event, char *message, void* context);
	event_callback_t event_callback_handler = nullptr;
	void* event_callback_context = nullptr;

	void registerEventHandler(event_callback_t handler, void* context)
	{
		event_callback_handler = handler;
		event_callback_context = context;
	}

	void fireEvent(nm_event_t event, char *message)
	{
		if (event_callback_handler == nullptr) return;
		event_callback_handler(event, message, event_callback_context);
	}
};

class B {
public:
	B(A& a) : a(a) {
		printf("B::B(A&)\n");
		a.registerEventHandler([] (nm_event_t event, char *message, void* context) {
			B* b = (B*)context;
			b->networkEventHandler(event, message);
		}, this);

}


void networkEventHandler(nm_event_t event, char *message) {
	printf("B::networkEventHandler %s\n", message);
}

private:
	A& a;
};

  

int main() {
	A a;
	B b(a);
	a.fireEvent(0, "hola");
	return 0;
}
```

The C++17 way
```c++
#include <stdio.h>
#include <stdlib.h>
#include <functional>

typedef int nm_event_t;

class A {
public:
	std::function<void(nm_event_t event, char *message)> 
		event_callback_handler = nullptr;

	void registerEventHandler(std::function<void(nm_event_t event, char *message)> handler)
	{
		event_callback_handler = handler;
	}

	void fireEvent(nm_event_t event, char *message)
	{
		if (event_callback_handler == nullptr) return;
		event_callback_handler(event, message);
	}
};


class B {
public:
	B(A& a) : a(a) {
		printf("B::B(A&)\n");
		a.registerEventHandler(
			std::bind(
				&B::networkEventHandler, 
				this, 
				std::placeholders::_1, 
				std::placeholders::_2
			)
		);
	}

	void networkEventHandler(nm_event_t event, char *message) {
		printf("B::networkEventHandler %s\n", message);
	}

private:
	A& a;
};

int main() {
	A a;
	B b(a);
	a.fireEvent(0, "hola");
	return 0;
}
```