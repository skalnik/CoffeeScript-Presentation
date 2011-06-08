!SLIDE center

#So what are some of the awesome features?#

!SLIDE bullets incremental

# Functions #

 * A much cleaner syntax
 * Default values
 * Implicit returns
 * Splats for variable number arguments

!SLIDE

    @@@javascript
    square = (x) -> x * x
    cube   = (x) -> (square x) * x

##Compiles to:##
    
    @@@javascript
    var cube, square;
    square = function(x) {
      return x * x;
    }
    cube = function(x) {
      return square(x) * x;
    }

!SLIDE

    @@@javascript
    fill = (container, liquid="coffee") ->
      "Filling #{contained} with #{liquid}"

##Compiles to:##
    
    @@@javascript
    var fill;
    fill = function(container, liquid) {
      if (liquid == null) {
        liquid = "coffee";
      }
      return "Filling " + container + 
             " with " + liquid;

!SLIDE small

    @@@javascript
    gold = silver = rest = "unknown"
    awardMedals = (first, second, others...) ->
      gold =   first
      silver = second
      rest =   others
    
##Compiles to: ##

    @@@javascript
    var awardMedals, gold, silver, rest;
    var __slice = Array.prototype.slice;
    gold = silver = rest = "unknown";
    awardMedals = function() {
      var first, second, others;
      first = arguments[0], second = arguments[1], 
        others = 3 <= arguments.length? 
        __slide.call(arguments, 2): [];
      gold = first;
      silver = second;
      return rest = others;
    }

!SLIDE bullets incremental

#Strings#

 * Ruby like interpolation
 * Multiline Strings
 * Heredocs (', ", and ##)

!SLIDE

    @@@javascript
    flavor = "Blue Raspberry"
    quote = "My favorite is #{flavor}"
    math = "#{22/7} is close to pi"

##Compiles to##

    @@@javascript
    var flavor, quote, math;
    flavor = "Blue Raspberry";
    quote = "My favorite flavor is " + flavor;
    math = "" + (22 / 7) + " is close to pi";

!SLIDE small
  
    @@@javascript
    multiline = "Whoa! Multiline strings are
      nifty!"
    code = '''
           <p>
             Double quote to use interpolation
           </p>
           '''
    ###
    Multiline
    Comments!
    ###

##Compiles to##

    @@@javascript
    var multiline, code;
    multiline = "Whoa! Multiline strings are nifty!";
    code = "<p>\n  Double quote to use interpolation\n<p>";
    /*
    Multiline
    Comments!
    */


!SLIDE bullets incremental

# Objects #

 * Object literals similar to JavaScript cousins
 * Optionally defined via indentation, like YAML

!SLIDE

    @@@javascript
    singers = { Jagger: "Rock", Elvis: "Roll" }
    family =
      sister:
        name: "Lucie"
        age:  32
      sister:
        name: "Penny"
        age:  31
      nephew:
        name: "Luke"
        age:  5

!SLIDE bullets incremental

# Conditionals #

 * No need for surrounding parens
 * Or surrounding braces
 * Inline if/then instead of ternary
 * And or=, like Ruby's ||=

!SLIDE

    @@@javascript
    if happy and knowsIt
      clapHands()
    else
      showIt()

##Compiles to##
    
    @@@javascript
    if (happy && knowsIt) {
        clapsHands();
    } else {
      showIt();
    }

!SLIDE

    @@@javascript
    date = if friday then sue else jill
    options or= defaults);

##Compiles to##

    @@@javascript
    date = friday ? sue : jill;
    options || (options = defaults);

!SLIDE bullets incremental

#Loops & Comprehensions#
 * Most loops will simply be comprehensions
 * They replace (and compile into) for loops

!SLIDE

    @@@javascript
    (eat food) for food in ['toast', 
                            'cheese',
                            'wine']

##Compiles to##

    @@@javascript
    var food, _i, _len, _ref;
    _ref = ['toast', 'cheese', 'wine'];
    for(_i = 0, _len = _ref.length; _i < _len;
                                    _i++) {
      food = _ref[_i];
      eat(food);
    }

!SLIDE

    @@@javascript
    shortNames = (name for name in list 
                           when name.length < 5)
    evens = (x for x in [0..10] by 2)

!SLIDE bullets incremental

#Classes & Inheritence#

 * Classical inheritance built on top of JavaScript's prototypes

!SLIDE code

    @@@javascript
    class Animal
      constructor: (@name) ->

      move: (meter) ->
        alert @name + " moved " + meters + "m."

    class Snake extends Animal
      move: ->
        alert "Slithering..."
        super 5

    class Horse extends Animal
      move: ->
        alert "Galloping..."
        super 45

!SLIDE bullets incremental

#Existential Operator#

 * `?` similar to Ruby's `nil?`

!SLIDE

    @@@javascript
    solipsism = true if mind? and not world?
    footprints = yeti ? "bear"

##Compiles to##

    @@@javascript
    if ((typeof mind !== "undefined" && 
        mind !== null) && 
        !(typeof world !=="undefined" &&
        world !== null)) {
      solipsism = true;
    }
    footprints = typeof yeti !== "undefined" &&
                   yeti !== null ? yeti : "bear";

!SLIDE bullets incremental

#Destructuring Assignment#

 * Implements proposed destructuring assignment

!SLIDE small

    @@@javascript
    theBait   = 1000
    theSwitch = 0

    [theBait, theSwitch] = [theSwitch, theBait]

    futurists = 
      sculptor: "Umberto Boccioni"
      painter:  "Vladimir Burliuk"
      poet:
        name: "F.T. Marinetti"
        address: [
          "Via Roma 42R"
          "Bellagio, Italy 22021"
        ]

    {poet: {name, address: [street, city]}} = futurists
    # Will assign name, street, and city properly

