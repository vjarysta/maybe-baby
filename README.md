# maybe-baby

[![Build Status](https://travis-ci.org/mikechabot/maybe-baby.svg?branch=master)](https://travis-ci.org/mikechabot/maybe-baby)
[![Coverage Status](https://coveralls.io/repos/github/mikechabot/maybe-baby/badge.svg?branch=master&cacheBuster=1)](https://coveralls.io/github/mikechabot/maybe-baby?branch=master)
[![Dependency Status](https://david-dm.org/mikechabot/maybe-baby.svg)](https://david-dm.org/mikechabot/maybe-baby)
[![devDependencies Status](https://david-dm.org/mikechabot/maybe-baby/dev-status.svg)](https://david-dm.org/mikechabot/maybe-baby?type=dev)

[![NPM](https://nodei.co/npm/maybe-baby.png)](https://nodei.co/npm/maybe-baby/)

`maybe-baby` is the [Maybe monad](https://en.wikipedia.org/wiki/Monad_(functional_programming)#The_Maybe_monad) implemented in JavaScript. 

Big credit to [James Sinclair](https://github.com/jrsinclair) for writing the blogpost [The Marvellously Mysterious JavaScript Maybe Monad](http://jrsinclair.com/articles/2016/marvellously-mysterious-javascript-maybe-monad/), which clicked for me in a way that other articles hadn't. I'd recommend giving it a read if you haven't yet already.

**Monad**
    
    var Maybe = function (val) {
        this.__value = val;
    };

    Maybe.of = function (val) {
        return new Maybe(val);
    };

    Maybe.prototype.isNothing = function () {
        return (this.__value === null || this.__value === undefined);
    };

    Maybe.prototype.isJust = function () {
        return !this.isNothing();
    };

    Maybe.prototype.join = function () {
        return this.__value;
    };

    Maybe.prototype.prop = function (property) {
        return this.map(
            function (value) {
                return value[property];
            }
        );
    };

    Maybe.prototype.map = function (transform) {
        if (this.isNothing()) {
            return Maybe.of(null);
        }
        return Maybe.of(transform(this.join()));
    };

    Maybe.prototype.orElse = function (defaultVal) {
        if (this.isNothing()) {
            return Maybe.of(defaultVal);
        }
        return this;
    };
