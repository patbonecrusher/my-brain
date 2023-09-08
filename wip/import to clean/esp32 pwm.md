All based on the timer.

Setting frequency:

```C
TIMER_TopSet(TIMER0, how_often_to_pulse);
```

Setting duty cycle:

```C
TIMER_CompareBufSet(TIMER0, 0, duty_cycle);
```

The following image shows duty cycle versus frequency (period)

![[Pasted image 20220902152544.png]]


When hooking up the interrupt, it will interrupt every period.  And the internal counter will be equal to the number of periods.