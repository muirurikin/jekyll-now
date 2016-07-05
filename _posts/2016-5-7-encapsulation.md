---
layout: post
title: Encapsulation
---
#### Accessor methods

Accessors (also known as getters and setters) are methods that let you read and write the value of an instance variable of an object.

publicclassAccessorExample {

privateStringattribute; 

publicStringgetAttribute() { 

returnattribute;

  } 

publicvoidsetAttribute(Stringattribute) { 

this.attribute=attribute;

  }

}

#### Why Accessors?

There are actually many good reasons to consider using accessors rather than directly exposing fields of a class

Getter and Setters make APIs more stable. For instance, consider a field public in a class which is accessed by other classes. Now later on, you want to add any extra logic while getting and setting the variable. This will impact the existing client that uses the API. So any changes to this public field will require change to each class that refers it. On the contrary, with accessor methods, one can easily add some logic like cache some data, lazily initialize it later. Moreover, one can fire a property changed event if the new value is different from the previous value. All this will be seamless to the class that gets value using accessor method.

#### Have Accessors For All Fiealds?

Fields can be declared public for package-private or private nested class. Exposing fields in these classes produces less visual clutter compare to accessor-method approach, both in the class definition and in the client code that uses it.

If a class is package-private or is a private nested class, there is nothing inherently wrong with exposing its data fields—assuming they do an adequate job of describing the abstraction provided by the class.

Such code is restricted to the package where the class is declared, while the client code is tied to class internal representation. We can change it without modifying any code outside that package. Moreover, in the case of a private nested class, the scope of the change is further restricted to the enclosing class.

Another example of a design that uses public fields is JavaSpace entry objects. Ken Arnold described the process they went through to decide to make those fields public instead of private with get and set methods [here](http://www.artima.com/intv/sway2.html)

Now this sometimes makes people uncomfortable because they've been told not to have public fields; that public fields are bad. And often, people interpret those things religiously. But we're not a very religious bunch. Rules have reasons. And the reason for the private data rule doesn't apply in this particular case. It is a rare exception to the rule. I also tell people not to put public fields in their objects, but exceptions exist. This is an exception to the rule, because it is simpler and safer to just say it is a field. We sat back and asked: Why is the rule thus? Does it apply? In this case it doesn't.

#### Private fields + Public accessors == encapsulation

Consider the example below

publicclassA {

publicinta;

}

Usually this is considered bad coding practice as it violates encapsulation. The alternate approach is

publicclassA {

privateinta; 

publicvoidsetA(inta) { 

this.a=a;

  } 

publicintgetA() { 

returnthis.a;

  }

}

It is argued that this encapsulates the attribute. Now is this really encapsulation?

Fact is, Getters/setters have nothing to do with encapsulation. Here the data isn't more hidden or encapsulated than it was in a public field. Other objects still have intimate knowledge of the internals of the class. Changes made to the class might ripple out and enforce changes in dependent classes. Getter and setter in this way are generally break encapsulation. A truly well-encapsulated class has no setters and preferably no getters either. Rather than asking a class for some data and then compute something with it, the class should be responsible to compute something with its data and then return the result.

Consider an example below,

publicclassScreens {

privateMapscreens=newHashMap(); 

publicMapgetScreens() { 

returnscreens;

  } 

publicvoidsetScreens(Mapscreens) { 

this.screens=screens;

  }

// remaining code here

}

If we need to get a particular screen, we do code like below,

Screens= (Screen)screens.get(screenId);

There are things worth noticing here....

The client needs to get an Object from the Map and casting it to the right type. Moreover, the worst is that any client of the Map has the power to clear it which may not be the case we usually want.

Alternative implementation of the same logic is:

publicclassScreens {

privateMapscreens=newHashMap(); 

publicScreengetById(Stringid) { 

return (Screen) screens.get(id);

  }

// remaining code here

}

Here the Map instance and the interface at the boundary (Map) are hidden.

#### Conclusions

Use of accessors to restrict direct access to field variable is preferred over the use of public fields, however, making getters and setter for each and every field is overkill. It also depends on the situation though, sometimes you just want a dumb data object. Accessors should be added for field where they're really required. A class should expose larger behavior which happens to use its state, rather than a repository of state to be manipulated by other classes.
