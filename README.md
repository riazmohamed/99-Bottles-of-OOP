# Sandi Metz - 99 Bottles of OOP

## Index

1. [Test suite](#test-suite)
2. [Incomprehensibly concise](#first-attempt)
3. [Speculative General](#speculative-general)

In this book the author is attempting to give us a broader overview of a value/cost analysis using different implementations. The set of value cost questions used here are 

* How difficult was it to write?
* How hard it is to understand?
* How expensive will it be to change?

### Test Suite

The following is the test suite against which the code will be executed. Here we are using the gem `Minitest` to test the application in `bottle.rb`

```ruby
gem 'minitest', '~> 5.4'
require 'minitest/autorun'
require 'minitest/reporters'
Minitest::Reporters.use!
require_relative '../lib/bottles'

class BottlesTest < Minitest::Test
  def test_the_first_verse
    expected =
      "99 bottles of milk on the wall, " +
      "99 bottles of milk.\n" +
      "Take one down and pass it around, " +
      "98 bottles of milk on the wall.\n"
    assert_equal expected, Bottles.new.verse(99)
  end

  def test_another_verse
    skip
    expected =
      "3 bottles of milk on the wall, " +
      "3 bottles of milk.\n" +
      "Take one down and pass it around, " +
      "2 bottles of milk on the wall.\n"
    assert_equal expected, Bottles.new.verse(3)
  end

  def test_verse_2
    skip
    expected =
      "2 bottles of milk on the wall, " +
      "2 bottles of milk.\n" +
      "Take one down and pass it around, " +
      "1 bottle of milk on the wall.\n"
    assert_equal expected, Bottles.new.verse(2)
  end

  def test_verse_1
    skip
    expected =
      "1 bottle of milk on the wall, " +
      "1 bottle of milk.\n" +
      "Take it down and pass it around, " +
      "no more bottles of milk on the wall.\n"
     assert_equal expected, Bottles.new.verse(1)
  end

  def test_verse_0
    skip
    expected =
      "No more bottles of milk on the wall, " +
      "no more bottles of milk.\n" +
      "Go to the store and buy some more, " +
      "99 bottles of milk on the wall.\n"
    assert_equal expected, Bottles.new.verse(0)
  end

  def test_a_couple_verses
    skip
    expected =
      "99 bottles of milk on the wall, " +
      "99 bottles of milk.\n" +
      "Take one down and pass it around, " +
      "98 bottles of milk on the wall.\n" +
      "\n" +
      "98 bottles of milk on the wall, " +
      "98 bottles of milk.\n" +
      "Take one down and pass it around, " +
      "97 bottles of milk on the wall.\n"
    assert_equal expected, Bottles.new.verses(99, 98)
  end

  def test_a_few_verses
    skip
    expected =
      "2 bottles of milk on the wall, " +
      "2 bottles of milk.\n" +
      "Take one down and pass it around, " +
      "1 bottle of milk on the wall.\n" +
      "\n" +
      "1 bottle of milk on the wall, " +
      "1 bottle of milk.\n" +
      "Take it down and pass it around, " +
      "no more bottles of milk on the wall.\n" +
      "\n" +
      "No more bottles of milk on the wall, " +
      "no more bottles of milk.\n" +
      "Go to the store and buy some more, " +
      "99 bottles of milk on the wall.\n"
    assert_equal expected, Bottles.new.verses(2, 0)
  end

  def test_the_whole_song
    skip
    expected = <<~SONG
      99 bottles of milk on the wall, 99 bottles of milk.
      Take one down and pass it around, 98 bottles of milk on the wall.

      98 bottles of milk on the wall, 98 bottles of milk.
      Take one down and pass it around, 97 bottles of milk on the wall.

      97 bottles of milk on the wall, 97 bottles of milk.
      Take one down and pass it around, 96 bottles of milk on the wall.

      96 bottles of milk on the wall, 96 bottles of milk.
      Take one down and pass it around, 95 bottles of milk on the wall.

      95 bottles of milk on the wall, 95 bottles of milk.
      Take one down and pass it around, 94 bottles of milk on the wall.

      94 bottles of milk on the wall, 94 bottles of milk.
      Take one down and pass it around, 93 bottles of milk on the wall.

      93 bottles of milk on the wall, 93 bottles of milk.
      Take one down and pass it around, 92 bottles of milk on the wall.

      92 bottles of milk on the wall, 92 bottles of milk.
      Take one down and pass it around, 91 bottles of milk on the wall.

      91 bottles of milk on the wall, 91 bottles of milk.
      Take one down and pass it around, 90 bottles of milk on the wall.

      90 bottles of milk on the wall, 90 bottles of milk.
      Take one down and pass it around, 89 bottles of milk on the wall.

      89 bottles of milk on the wall, 89 bottles of milk.
      Take one down and pass it around, 88 bottles of milk on the wall.

      88 bottles of milk on the wall, 88 bottles of milk.
      Take one down and pass it around, 87 bottles of milk on the wall.

      87 bottles of milk on the wall, 87 bottles of milk.
      Take one down and pass it around, 86 bottles of milk on the wall.

      86 bottles of milk on the wall, 86 bottles of milk.
      Take one down and pass it around, 85 bottles of milk on the wall.

      85 bottles of milk on the wall, 85 bottles of milk.
      Take one down and pass it around, 84 bottles of milk on the wall.

      84 bottles of milk on the wall, 84 bottles of milk.
      Take one down and pass it around, 83 bottles of milk on the wall.

      83 bottles of milk on the wall, 83 bottles of milk.
      Take one down and pass it around, 82 bottles of milk on the wall.

      82 bottles of milk on the wall, 82 bottles of milk.
      Take one down and pass it around, 81 bottles of milk on the wall.

      81 bottles of milk on the wall, 81 bottles of milk.
      Take one down and pass it around, 80 bottles of milk on the wall.

      80 bottles of milk on the wall, 80 bottles of milk.
      Take one down and pass it around, 79 bottles of milk on the wall.

      79 bottles of milk on the wall, 79 bottles of milk.
      Take one down and pass it around, 78 bottles of milk on the wall.

      78 bottles of milk on the wall, 78 bottles of milk.
      Take one down and pass it around, 77 bottles of milk on the wall.

      77 bottles of milk on the wall, 77 bottles of milk.
      Take one down and pass it around, 76 bottles of milk on the wall.

      76 bottles of milk on the wall, 76 bottles of milk.
      Take one down and pass it around, 75 bottles of milk on the wall.

      75 bottles of milk on the wall, 75 bottles of milk.
      Take one down and pass it around, 74 bottles of milk on the wall.

      74 bottles of milk on the wall, 74 bottles of milk.
      Take one down and pass it around, 73 bottles of milk on the wall.

      73 bottles of milk on the wall, 73 bottles of milk.
      Take one down and pass it around, 72 bottles of milk on the wall.

      72 bottles of milk on the wall, 72 bottles of milk.
      Take one down and pass it around, 71 bottles of milk on the wall.

      71 bottles of milk on the wall, 71 bottles of milk.
      Take one down and pass it around, 70 bottles of milk on the wall.

      70 bottles of milk on the wall, 70 bottles of milk.
      Take one down and pass it around, 69 bottles of milk on the wall.

      69 bottles of milk on the wall, 69 bottles of milk.
      Take one down and pass it around, 68 bottles of milk on the wall.

      68 bottles of milk on the wall, 68 bottles of milk.
      Take one down and pass it around, 67 bottles of milk on the wall.

      67 bottles of milk on the wall, 67 bottles of milk.
      Take one down and pass it around, 66 bottles of milk on the wall.

      66 bottles of milk on the wall, 66 bottles of milk.
      Take one down and pass it around, 65 bottles of milk on the wall.

      65 bottles of milk on the wall, 65 bottles of milk.
      Take one down and pass it around, 64 bottles of milk on the wall.

      64 bottles of milk on the wall, 64 bottles of milk.
      Take one down and pass it around, 63 bottles of milk on the wall.

      63 bottles of milk on the wall, 63 bottles of milk.
      Take one down and pass it around, 62 bottles of milk on the wall.

      62 bottles of milk on the wall, 62 bottles of milk.
      Take one down and pass it around, 61 bottles of milk on the wall.

      61 bottles of milk on the wall, 61 bottles of milk.
      Take one down and pass it around, 60 bottles of milk on the wall.

      60 bottles of milk on the wall, 60 bottles of milk.
      Take one down and pass it around, 59 bottles of milk on the wall.

      59 bottles of milk on the wall, 59 bottles of milk.
      Take one down and pass it around, 58 bottles of milk on the wall.

      58 bottles of milk on the wall, 58 bottles of milk.
      Take one down and pass it around, 57 bottles of milk on the wall.

      57 bottles of milk on the wall, 57 bottles of milk.
      Take one down and pass it around, 56 bottles of milk on the wall.

      56 bottles of milk on the wall, 56 bottles of milk.
      Take one down and pass it around, 55 bottles of milk on the wall.

      55 bottles of milk on the wall, 55 bottles of milk.
      Take one down and pass it around, 54 bottles of milk on the wall.

      54 bottles of milk on the wall, 54 bottles of milk.
      Take one down and pass it around, 53 bottles of milk on the wall.

      53 bottles of milk on the wall, 53 bottles of milk.
      Take one down and pass it around, 52 bottles of milk on the wall.

      52 bottles of milk on the wall, 52 bottles of milk.
      Take one down and pass it around, 51 bottles of milk on the wall.

      51 bottles of milk on the wall, 51 bottles of milk.
      Take one down and pass it around, 50 bottles of milk on the wall.

      50 bottles of milk on the wall, 50 bottles of milk.
      Take one down and pass it around, 49 bottles of milk on the wall.

      49 bottles of milk on the wall, 49 bottles of milk.
      Take one down and pass it around, 48 bottles of milk on the wall.

      48 bottles of milk on the wall, 48 bottles of milk.
      Take one down and pass it around, 47 bottles of milk on the wall.

      47 bottles of milk on the wall, 47 bottles of milk.
      Take one down and pass it around, 46 bottles of milk on the wall.

      46 bottles of milk on the wall, 46 bottles of milk.
      Take one down and pass it around, 45 bottles of milk on the wall.

      45 bottles of milk on the wall, 45 bottles of milk.
      Take one down and pass it around, 44 bottles of milk on the wall.

      44 bottles of milk on the wall, 44 bottles of milk.
      Take one down and pass it around, 43 bottles of milk on the wall.

      43 bottles of milk on the wall, 43 bottles of milk.
      Take one down and pass it around, 42 bottles of milk on the wall.

      42 bottles of milk on the wall, 42 bottles of milk.
      Take one down and pass it around, 41 bottles of milk on the wall.

      41 bottles of milk on the wall, 41 bottles of milk.
      Take one down and pass it around, 40 bottles of milk on the wall.

      40 bottles of milk on the wall, 40 bottles of milk.
      Take one down and pass it around, 39 bottles of milk on the wall.

      39 bottles of milk on the wall, 39 bottles of milk.
      Take one down and pass it around, 38 bottles of milk on the wall.

      38 bottles of milk on the wall, 38 bottles of milk.
      Take one down and pass it around, 37 bottles of milk on the wall.

      37 bottles of milk on the wall, 37 bottles of milk.
      Take one down and pass it around, 36 bottles of milk on the wall.

      36 bottles of milk on the wall, 36 bottles of milk.
      Take one down and pass it around, 35 bottles of milk on the wall.

      35 bottles of milk on the wall, 35 bottles of milk.
      Take one down and pass it around, 34 bottles of milk on the wall.

      34 bottles of milk on the wall, 34 bottles of milk.
      Take one down and pass it around, 33 bottles of milk on the wall.

      33 bottles of milk on the wall, 33 bottles of milk.
      Take one down and pass it around, 32 bottles of milk on the wall.

      32 bottles of milk on the wall, 32 bottles of milk.
      Take one down and pass it around, 31 bottles of milk on the wall.

      31 bottles of milk on the wall, 31 bottles of milk.
      Take one down and pass it around, 30 bottles of milk on the wall.

      30 bottles of milk on the wall, 30 bottles of milk.
      Take one down and pass it around, 29 bottles of milk on the wall.

      29 bottles of milk on the wall, 29 bottles of milk.
      Take one down and pass it around, 28 bottles of milk on the wall.

      28 bottles of milk on the wall, 28 bottles of milk.
      Take one down and pass it around, 27 bottles of milk on the wall.

      27 bottles of milk on the wall, 27 bottles of milk.
      Take one down and pass it around, 26 bottles of milk on the wall.

      26 bottles of milk on the wall, 26 bottles of milk.
      Take one down and pass it around, 25 bottles of milk on the wall.

      25 bottles of milk on the wall, 25 bottles of milk.
      Take one down and pass it around, 24 bottles of milk on the wall.

      24 bottles of milk on the wall, 24 bottles of milk.
      Take one down and pass it around, 23 bottles of milk on the wall.

      23 bottles of milk on the wall, 23 bottles of milk.
      Take one down and pass it around, 22 bottles of milk on the wall.

      22 bottles of milk on the wall, 22 bottles of milk.
      Take one down and pass it around, 21 bottles of milk on the wall.

      21 bottles of milk on the wall, 21 bottles of milk.
      Take one down and pass it around, 20 bottles of milk on the wall.

      20 bottles of milk on the wall, 20 bottles of milk.
      Take one down and pass it around, 19 bottles of milk on the wall.

      19 bottles of milk on the wall, 19 bottles of milk.
      Take one down and pass it around, 18 bottles of milk on the wall.

      18 bottles of milk on the wall, 18 bottles of milk.
      Take one down and pass it around, 17 bottles of milk on the wall.

      17 bottles of milk on the wall, 17 bottles of milk.
      Take one down and pass it around, 16 bottles of milk on the wall.

      16 bottles of milk on the wall, 16 bottles of milk.
      Take one down and pass it around, 15 bottles of milk on the wall.

      15 bottles of milk on the wall, 15 bottles of milk.
      Take one down and pass it around, 14 bottles of milk on the wall.

      14 bottles of milk on the wall, 14 bottles of milk.
      Take one down and pass it around, 13 bottles of milk on the wall.

      13 bottles of milk on the wall, 13 bottles of milk.
      Take one down and pass it around, 12 bottles of milk on the wall.

      12 bottles of milk on the wall, 12 bottles of milk.
      Take one down and pass it around, 11 bottles of milk on the wall.

      11 bottles of milk on the wall, 11 bottles of milk.
      Take one down and pass it around, 10 bottles of milk on the wall.

      10 bottles of milk on the wall, 10 bottles of milk.
      Take one down and pass it around, 9 bottles of milk on the wall.

      9 bottles of milk on the wall, 9 bottles of milk.
      Take one down and pass it around, 8 bottles of milk on the wall.

      8 bottles of milk on the wall, 8 bottles of milk.
      Take one down and pass it around, 7 bottles of milk on the wall.

      7 bottles of milk on the wall, 7 bottles of milk.
      Take one down and pass it around, 6 bottles of milk on the wall.

      6 bottles of milk on the wall, 6 bottles of milk.
      Take one down and pass it around, 5 bottles of milk on the wall.

      5 bottles of milk on the wall, 5 bottles of milk.
      Take one down and pass it around, 4 bottles of milk on the wall.

      4 bottles of milk on the wall, 4 bottles of milk.
      Take one down and pass it around, 3 bottles of milk on the wall.

      3 bottles of milk on the wall, 3 bottles of milk.
      Take one down and pass it around, 2 bottles of milk on the wall.

      2 bottles of milk on the wall, 2 bottles of milk.
      Take one down and pass it around, 1 bottle of milk on the wall.

      1 bottle of milk on the wall, 1 bottle of milk.
      Take it down and pass it around, no more bottles of milk on the wall.

      No more bottles of milk on the wall, no more bottles of milk.
      Go to the store and buy some more, 99 bottles of milk on the wall.
    SONG
    assert_equal expected, Bottles.new.song
  end
end
```



### First attempt 

### Incomprehensibly concise

```ruby
class Bottles
  def song
    verses(99, 0)
  end

  def verses(hi, lo)
    hi.downto(lo).map {|n| verse(n) }.join("\n")
  end

  def verse(n)
     "#{n == 0 ? 'No more' : n} bottle#{'s' if n != 1}" +
     " of milk on the wall, " +
     "#{n == 0 ? 'no more' : n} bottle#{'s' if n != 1} of milk.\n" +
    "#{n > 0  ? "Take #{n > 1 ? 'one' : 'it'} down and pass it around"
               : "Go to the store and buy some more"}, " +
     "#{n-1 < 0 ? 99 : n-1 == 0 ? 'no more' : n-1} bottle#{'s' if n-1 != 1}"+
     " of milk on the wall.\n"
  end
end
```

In the above code though the above code is very concise it is very hard to read and due to this it is hard to maintain. The above should be avoided in order to reduce the cost in the long run. The above code does not follow the principles of `DRY`.

### Second attempt

### Speculative General

```ruby
class Bottles
  NoMore = lambda do |verse|
   "No more bottles of milk on the wall, " +
   "no more bottles of milk.\n" +
  "Go to the store and buy some more, " +
   "99 bottles of milk on the wall.\n"
  end

  LastOne = lambda do |verse|
   "1 bottle of milk on the wall, " +
   "1 bottle of milk.\n" +
   "Take it down and pass it around, " +
   "no more bottles of milk on the wall.\n"
  end

  Penultimate = lambda do |verse|
   "2 bottles of milk on the wall, " +
   "2 bottles of milk.\n" +
   "Take one down and pass it around, " +
   "1 bottle of milk on the wall.\n"
  end

  Default = lambda do |verse|
   "#{verse.number} bottles of milk on the wall, " +
   "#{verse.number} bottles of milk.\n" +
   "Take one down and pass it around, " +
   "#{verse.number - 1} bottles of milk on the wall.\n"
  end

  def song
   verses(99, 0)
  end

  def verses(finish, start)
   (finish).downto(start).map {|verse_number|
     verse(verse_number) }.join("\n")
  end

  def verse(number)
   verse_for(number).text
  end

  def verse_for(number)
   case number
   when 0 then Verse.new(number, &NoMore)
   when 1 then Verse.new(number, &LastOne)
   when 2 then Verse.new(number, &Penultimate)
   else        
     Verse.new(number, &Default)
   end
  end
end
 
class Verse
 attr_reader :number
 def initialize(number, &lyrics)
   @number = number
   @lyrics = lyrics
 end

 def text
   @lyrics.call self
 end
end
```

The complexity in the above code is quite high due to its depndencies. The above should be avoided and one must strive to write a much simpler solution.  



### Concretely abstract

Naming the methods with wrong layer of abstractions

```ruby
class Bottles
  def song
    verses(99, 0)
  end

  def verses(bottles_at_start, bottles_at_end)
    bottles_at_start.downto(bottles_at_end).map do |bottles|
      verse(bottles)
    end.join("\n")
  end

  def verse(bottles)
    Round.new(bottles).to_s
  end
end

class Round
  attr_reader :bottles
  def initialize(bottles)
    @bottles = bottles
  end

  def to_s
    challenge + response
  end

  def challenge
    bottles_of_milk.capitalize + " " + on_wall + ", " +
    bottles_of_milk + ".\n"
  end

  def response
    go_to_the_store_or_take_one_down + ", " +
    bottles_of_milk + " " + on_wall + ".\n"
  end

  def bottles_of_milk
    "#{anglicized_bottle_count} #{pluralized_bottle_form} of #{milk}"
  end

  def milk
    "milk"
  end

  def on_wall
    "on the wall"
  end

  def pluralized_bottle_form
    last_milk? ? "bottle" : "bottles"
  end

  def anglicized_bottle_count
    all_out? ? "no more" : bottles.to_s
  end

  def go_to_the_store_or_take_one_down
    if all_out?
      @bottles = 99
      buy_new_milk
    else
      lyrics = drink_milk
      @bottles -= 1
      lyrics
    end
  end

  def buy_new_milk
    "Go to the store and buy some more"
  end

  def drink_milk
    "Take #{it_or_one} down and pass it around"
  end

  def it_or_one
    last_milk? ? "it" : "one"
  end

  def all_out?
    bottles.zero?
  end

  def last_milk?
    bottles == 1
  end
end
```

Here we are attempting to create a solution which follows the `DRY` principle. However care should be taken in naming the methods appropriately. The main point taken from the above code is that in-order for the code to reduce cost and to truly follow the `DRY` principle **the methods should be named after what they mean and what they represent in the context of the problem domain and not based on what they do**. Naming the method at a slightly higher level of abstraction negates the need to change the method name when we change the context of the program. 

```ruby
drink = "Milk"

def milk_shake(drink)
  drink
end
```

In the above code everytime we would like to change the beverage we will have to change the method name so that everything is in the context of the domain.

```ruby
drink = "kool-aid"

def beverage(drink)
  drink
end
```

In the above code since we have a higher layer of abstraction in the method name the previous problem is now negated. Naming the methods with the wrong layer of abstraction can lead to a higher cost when changing the implementation details. The main lesson learnt from this implementation detail is that the methods should be named based on the concepts they represent and not based on how they currently behave. Also the current solution does not address the value/cost question as many of the methods have wrong abstractions.
