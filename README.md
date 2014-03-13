AOP
===

A small Aspect Oriented Programming JavaScript library

In our search for a simple AOP library in JavaScript we evaluated several solutions and decided to use Fredrik Appelberg's excellent [Aop.js](http://fredrik.appelberg.me/2010/05/07/aop-js.html). We found that instead of passing JavaScript objects into the namespaces parameter we needed to pass an object prototype in, so all instances of our object's methods were intercepted by the aspect. Only a couple of very minor modifications were needed for this, so credit is entirely due here to Fredrik's library. With his kind permission I have published our modified version of the library.

How to use (assume 'cat' objects with prototype 'makeSound'...):

		var Cat = function(){
		  this.makeSound = function(){ 
		    console.log('Meooowwww!');
		  }; 
		};
		
		Cat.prototype.test = function(){ console.log('test-proto') }
		
		var test = new Cat;
		
		Aop.before("test", function() {
		      console.log('aop-test', arguments );
		}, [ Cat.prototype ]);
		
		Aop.before("makeSound", function() {
		      console.log('aop-sound', arguments);
		}, [ test ]);
		
		test.makeSound(2,56 );
		test.test();

License: MIT
