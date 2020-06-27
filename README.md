# Minimal Elixir Style Guide 

## Table of contents

* __[Modules](#about)__
  * [Ordering](#ordering)
  * [Grouping and spacing](#grouping-and-spacing)
  * [Always alias modules before calling them](#always-alias-modules-before-calling-them)
  * [Use `__MODULE__` when possible and group namespaces](#use-`__MODULE__`-when-possible-and-group-namespaces)
* __[Functions](#functions)__
  * [Avoid single pipes](#avoid-single-pipes)
  * [Start pipe-chains with raw value](#start-pipe-chains-with-raw-value)
  * [Use short syntax for one-liners](#use-short-syntax-for-one-liners)
  * [Always use parentheses for 0-arity function declarations and calls](#always-use-parentheses-for-0-arity-function-declarations-and-calls)
* __[Testing](#testing)__
  * [Assertions: function under test to the left, expected value on the right](#assertions-function-under-test-to-the-left-expected-value-on-the-right)
  * [Clearly distinguish phases of a test with spacing](#clearly-distinguish-phases-of-a-test-with-spacing)
  * [Use describe blocs to group related tests](#use-describe-blocs-to-group-related-tests)
  * [Test documentation](#test-documentation)


## Modules

### Ordering

```elixir
defmodule MyMod do
  @moduledoc
  
  @behaviour
  
  use
  
  import
  
  alias
  
  require
  
  @module_attribute
  
  defstruct
 
  @type
  
  @callback
  
  @macrocallback
  
  @optional_callbacks
  
  defmacro, def, etc...
end
```

### Grouping and spacing

```elixir
use

import

alias
alias

require
```
		
### Always alias modules before calling them

```elixir
# bad 
defmodule MyMod do
  def my_func(), do: MyOtherMod.my_other_func()
end 

# good 
defmodule MyMod do
  alias MyOtherMod
  
  def my_func(), do: MyOtherMod.my_other_func()
end
```
    
### Use `__MODULE__` when possible and group namespaces

```elixir
# bad
defmodule MyMod do
  alias MyMod.MyOtherMod
  alias MyMod.YetAnotherMod
end

# good
defmodule MyMod do
  alias __MODULE__.{MyOtherMod, YetAnotherMod}
end
```
   
## Functions

### Avoid single pipes

```elixir
# bad
val |> my_func()

# good
my_func(val)
```
    
### Start pipe-chains with raw value

```elixir
# bad
func(val) |> another_func() |> ...

# good
val |> func() |> another_func |> ...
```

### Use short syntax for one-liners

```elixir
# bad
def my_func() do
  "Hello World!"
end

# good
def my_func(), do: "Hello world!"
```
    
### Always use parentheses for 0-arity function declarations and calls

```elixir
# bad
def my_func, do: my_other_func

# good 
def my_func(), do: my_other_func()
```    
    
## Testing

### Assertions: function under test to the left, expected value on the right

```elixir
# bad
assert nil == my_func()

# good
assert my_func() == nil

# exception: pattern match
assert {:ok, val} = my_func
```

### Clearly distinguish phases of a test with spacing

```elixir
# bad
test "my test" do
  var = 1
  
  my_other_var = true
  assert var == 1
  
  assert my_other_var == true
end

# good
test "my test" do
  var = 1
  my_other_var = true
  
  assert var == 1
  assert my_other_var == true
end
```
  
### Use describe blocs to group related tests

```elixir
# bad
test "my_func/1 with option A" do
  ...
end
  
test "my_func/1 with option B" do
  ...
end
  
# good
describe "my_func/1:" do
  test "with option A" do
    ...
  end

  test "with option B" do
   ...
  end
end
```
	    
### Test documentation

```elixir
defmodule MyMod do
  @doc """
  Returns `"hello world!"`.
  
  ## Example
  
      iex> my_func()
      "hello world!"    
  """
  def my_func(), do: "hello world!"
end

defmodule MyModTest do
  doctest
	
  test "my_func/0" do
    ...
  end
end
```
