[[Miscellaneous]]
## Description
```
Calculator
Misc
Worth 777 Points
By ronnie
```

Find the flag.

Flag Format: CIT{example_flag}

Then there's an attached calculator.lua file which contains
```
function calculate(num1,num2,operator)

    if operator == "+" then

        return num1 + num2

    elseif operator == "-" then

        return num1 - num2

    elseif operator == "*" then

        return num1 * num2

    elseif operator == "/" then

        if num2 == 0 then

            return "Error: Division by zero is not allowed."

        else

            return num1 / num2

        end

    else

        return "Error: Invalid operator."

    end

end

  

io.write("Enter the first number: ")

local input1 = io.read()

local number1 = tonumber(input1)

if not number1 then

    print("Invalid input. Please enter a valid number.")

    os.exit(1)

end

  

io.write("Enter an operator (+, -, *, /): ")

local operator = io.read()

  

io.write("Enter the second number: ")

local input2 = io.read()

local number2 = tonumber(input2)

if not number2 then

    print("Invalid input. Please enter a valid number.")

    os.exit(1)

end

  

local result = calculate(number1, number2, operator)

  

print("Result: " .. tostring(result))

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

  
  
  
  

-- nope no flag here, keep looking :P
```

![[calculator (1) 1.lua]]

## Solution

After looking through the file I found it suspicious that there were 70 or so extra lines, so I selected them and noticed that from line 80-114 there were hidden spaces and tabs which immediately reminded of whitespace code.

## Flag

So by putting lines 80-114 into https://www.dcode.fr/whitespace-language you get the correct flag:
CIT{hft4bT0415Lb}