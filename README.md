A fork to [evilbocchi's library](https://github.com/evilbocchi/alyanum).
Primary difference is that it supports percentages(relative to DECIMAL_POINTS, found inside the module).


#### Example with fromPercent & toPercent:
```luau
local AN = require("./path/to/AlyaNum")

--[[
@param fromPercent automatically detects numbers meaning % can be omitted when using fromPercent
You can use scientific notation for example(1e10)
]]
local a = AN.fromString("100")
local b = AN.fromPercent("10%")

print(a + b) -- should print 110

--You can also add percentages
print(b + b) -- should print 0.2(10% + 10%)

-- 2 methods of converting to percentage
print(a:toPercent()) -- should print 5000%
print(AlyaNum.toPercent(AlyaNum.fromString("5.52"))) -- should print 552%

-- testing with some large numbers
print(AlyaNum.fromPercent("1e10000000000000000000000000%") + AlyaNum.fromPercent("1e10000000000000000000000000%")) -- should print 1e10Sp
print(AlyaNum.fromPercent("1e10000000000%") ^ AlyaNum.fromPercent("1e100")) -- should print 1e999.999QdTg
```


#### Example with getPercentage:
Will always return from 0% to 100%
This passes all the test by the way.
```luau
local AN = require("./path/to/Alyanum")

-- 🟢 Normal Cases
print("50 / 100:", AN.getPercentage(AN.new(50), AN.new(100))) -- 0.5
print("75 / 300:", AN.getPercentage(AN.new(75), AN.new(300))) -- 0.25

-- 🟢 Clamping Cases
print("200 / 100 (Clamp to 1):", AN.getPercentage(AN.new(200), AN.new(100))) -- 1
print("-50 / 100 (Clamp to 0):", AN.getPercentage(AN.new(-50), AN.new(100))) -- 0

-- 🟢 Edge Cases (NaN, Inf, Div by Zero)
print("NaN / 100:", AN.getPercentage(AlyaNum.new(0), AN.new(100))) -- 0
print("100 / Inf:", AN.getPercentage(AlyaNum.new(100), AN.new(math.huge))) -- 0
print("50 / 0 (Div by Zero):", AN.getPercentage(AlyaNum.new(50), AN.new(0))) -- 0

-- 🟢 Negative Edge Cases
print("-100 / 500 (Negative min):", AN.getPercentage(AN.new(-100), AN.new(500))) -- 0
print("100 / -500 (Negative max):", AN.getPercentage(AN.new(100), AN.new(-500))) -- 0
print("-50 / -100 (Both Negative):", AN.getPercentage(AN.new(-50), AN.new(-100))) -- 0.5
print("-100 / -50 (Min > Max, Clamp to 1):", AN.getPercentage(AN.new(-100), AN.new(-50))) -- 1

-- 🟢 Checking Decimal Precision (Rounded to 3 Places)
print("33 / 100:", AN.getPercentage(AN.new(33), AN.new(100))) -- Expected: 0.33
print("99 / 300:", AN.getPercentage(AN.new(99), AN.new(300))) -- Expected: 0.33
print("1 / 3:", AN.getPercentage(AN.new(1), AN.new(3))) -- Expected: 0.33
print("2 / 3:", AN.getPercentage(AN.new(2), AN.new(3))) -- Expected: 0.66
print("1 / 6:", AN.getPercentage(AN.new(1), AN.new(6))) -- Expected: 0.16
print("7 / 8:", AN.getPercentage(AN.new(7), AN.new(8))) -- Expected: 0.87
print("1 / 7:", AN.getPercentage(AN.new(1), AN.new(7))) -- Expected: 0.14
print("22 / 7:", AN.getPercentage(AN.new(22), AN.new(7))) -- Expected: 1

-- 🟢 Small Values
print("0.1 / 1:", AN.getPercentage(AN.new(0.1), AN.new(1))) -- Expected: 0.1
print("0.005 / 1:", AN.getPercentage(AN.new(0.005), AN.new(1))) -- Expected: 0
print("0.0003 / 1:", AN.getPercentage(AlyaNum.new(0.0003), AN.new(1))) -- Expected: 0

-- 🟢 Large Values
print("999999 / 1000000:", AN.getPercentage(AN.new(999999), AN.new(1000000))) -- Expected: 1
print("123456 / 654321:", AN.getPercentage(AN.new(123456), AN.new(654321))) -- Expected: 0.18
print("98765 / 123456:", AN.getPercentage(AN.new(98765), AN.new(123456))) -- Expected: 0.8
```
