!SLIDE bullets incremental

* JavaScript is hard to avoid
* Coming from Ruby, the syntax can seem ugly
* The semicolons stab my eyes!

!SLIDE

# CoffeeScript to the rescue! #

!SLIDE bullets incremental

# CoffeeScript #

* "It's just Javascript"
* Similar to haml for HTML
* or sass for CSS

!SLIDE bullets incremental

* Compiles down to JavaScript
* Brings in ideas from Ruby & Python
* Whitespace sensitive (Yay! Boo!)

!SLIDE

    @@@javascript
    window.Money = class Money
      constructor: (rawString) ->
        @cents = @parseCents rawString
    
      parseCents: (rawString="") ->
        [dollars, cents] = 
                rawString.match(/(\d+)/g) ? [0,0]
        + cents + 100 * dollars

!SLIDE small code

    @@@javascript
    (function() {
      var Money;
      window.Money = Money = (function() {
        function Money(rawString) {
          this.cents = this.parseCents(rawString);
        }
        Money.prototype.parseCents = 
                         function(rawString) {
          var cents, dollars, _ref, _ref2;
          if (rawString == null) {
            rawString = "";
          }
          _ref2 = (_ref = rawString.match(/(\d+)/g)) != null ? 
              _ref : [0, 0], 
              dollars = _ref2[0], cents = _ref2[1];
          return +cents + 100 * dollars;
        };
        return Money;
      })();
    }).call(this); 
