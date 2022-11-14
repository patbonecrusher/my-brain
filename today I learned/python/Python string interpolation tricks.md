---
creation date: 2022-11-14 13:43
modification date: Monday 14th November 2022 13:43:45
tags: engineering/coding/python, today_i_leaned
---

# Python string interpolation tricks

```python
text = 'EPIC'

print(f'{text}')
# output: EPIC

print(f'{text:#<20}')
print(f'{text:_>20}')
print(f'{text:.^20}')

# output: EPIC################
# output: ________________EPIC
# output: ........EPIC........

```