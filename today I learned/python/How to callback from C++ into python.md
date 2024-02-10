---
creation date: 2024-02-09 22:30
modification date: Friday, 9th February 2024, 22:30:11
tags:
  - today_i_leaned
  - engineering/coding/python
  - computer/language/cpp
---

```cpp
#pragma once

#include <atomic>
#include <chrono>
#include <functional>
#include <thread>

class System
{
public:
  using Callback = std::function<void(int)>;
  System(): t_(), cb_(), stop_(true) {}
  ~System()
  {
    stop();
  }
  bool start()
  {
    if (t_.joinable()) return false;
    stop_ = false;
    t_ = std::thread([this]()
    {
      while (!stop_)
      {
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
        if (cb_) cb_(1234);
      }
    });
    return true;
  }
  bool stop()
  {
    if (!t_.joinable()) return false;
    stop_ = true;
    t_.join();
    return true;
  }
  bool registerCallback(Callback cb)
  {
    if (t_.joinable()) return false;
    cb_ = cb;
    return true;
  }

private:
  std::thread t_;
  Callback cb_;
  std::atomic_bool stop_;
};
```

```cpp
#include <iostream>
#include "system.hpp"

int g_counter = 0;

void foo(int i)
{
  std::cout << i << std::endl;
  g_counter++;
}

int main()
{
  System s;
  s.registerCallback(foo);
  s.start();
  while (g_counter < 3)
  {
    std::this_thread::sleep_for(std::chrono::milliseconds(1));
  }
  s.stop();
  return 0;
}
```

```cpp
#include "pybind11/functional.h"
#include "pybind11/pybind11.h"

#include "system.hpp"

namespace py = pybind11;

PYBIND11_MODULE(mysystembinding, m) {
  py::class_<System>(m, "System")
    .def(py::init<>())
    .def("start", &System::start, py::call_guard<py::gil_scoped_release>())
    .def("stop", &System::stop, py::call_guard<py::gil_scoped_release>())
    .def("registerCallback", &System::registerCallback);
}
```

```python
#!/usr/bin/env python

import mysystembinding
import time

g_counter = 0

def foo(i):
  global g_counter
  print(i)
  g_counter = g_counter + 1

s = mysystembinding.System()
s.registerCallback(foo)
s.start()
while g_counter < 3:
  time.sleep(1)
s.stop()
```


---
#### References

```cardlink
url: https://stackoverflow.com/questions/60410178/how-to-invoke-python-function-as-a-callback-inside-c-thread-using-pybind11
title: "How to invoke Python function as a callback inside C++ thread using pybind11"
description: "I designed a C++ system that invokes user defined callbacks from procedure running in a separate thread. Simplified system.hpp looks like this:#pragma once#include &lt;atomic&gt;#include &lt;c..."
host: stackoverflow.com
image: https://cdn.sstatic.net/Sites/stackoverflow/Img/apple-touch-icon@2.png?v=73d79a89bded
```

```cardlink
url: https://github.com/ikuokuo/start-pybind11/blob/master/docs/cpp_thread_callback_python_function.md
title: "start-pybind11/docs/cpp_thread_callback_python_function.md at master · ikuokuo/start-pybind11"
description: "Start pybind11. Contribute to ikuokuo/start-pybind11 development by creating an account on GitHub."
host: github.com
favicon: https://github.githubassets.com/favicons/favicon.svg
image: https://opengraph.githubassets.com/c07fef69a677632e835edb0225f00721cf618f83c52cf0bf14bc73a8fab1d175/ikuokuo/start-pybind11
```

