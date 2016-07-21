# HitBox.

[![Join the chat at https://gitter.im/SDGophers/2015-04-challenge](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/SDGophers/2015-04-challenge?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

The challenge for April meeting of SDGophers is to create an old visitor counter.
Back in prehistory (late 90's early 2000's) of internet, websites would display
the number of people had visited by showing a counter. This counter was usually
graphical and the image of the number could be customized with fonts and colours.

For this exercise you are going to implement such a counter. Just like last week
this challenge will come with five stages. For the meetup we only expect you to
complete the 100 visitors level.

Good luck.

## 100 Vistors

Create a web service using only the standard library, that when you hit a particular
url it will return an png counting the number of times that url has been hit. Use
the given png encoding the numbers 0-9, and the characters ",." to create the digits to display.

![Numbers Mask](https://raw.githubusercontent.com/SDGophers/2015-04-challenge/master/images/numbers.png)

This is a 300x400 px image, with each glyph being 100x100 px.

The url should look like the following:

GET http://localhost:8080/counter/${{identifier}}

Where identifier can be anything., but the count for each _identifier_ should be
unique.

If the url is sent a DELETE method it should reset the counter to zero.

DELETE http://localhost:8080/counter/${{identifer}}


For this exercise you should be able to do everything using only the standard 
libraries. There should be not reason to use anything outside of the standard
library.

extra credit: See if you can support other formats other then an png. 
Use either the extension (${{identifier}}.png, or Accept Header).

### References
* [image documentation](http://godoc.org/image)
* [image/draw documentation](http://godoc.org/image/draw)
* [net/http documentation](http://godoc.org/net/http)
* [Blog post on how to use image/draw standard library](http://blog.golang.org/go-imagedraw-package)


## 1,000 Vistors

You have new customers. Getting new customers is great, but now they want you to
have a different count for each site. Using the referer header, make the counter
for each identifier different for each different referer domain.



## 10,000 Vistors

You hit-counter is doing gang busters and everyone is using it. However, it seems
that the count will reset to zero every so often. After some time it's discovered
that this happens every time the server is restarted. Your boss wants you to save
the values, so that if the server needs to be restarted it will not lose the count
for each identifier.

Oh, and while you are at it, can you make it so that the count is not only for 
unique visitors. How are you going to handle resets for this? 

To reset a specific referer counter, the delete command should it:
/counter/${{identifier}}/${{refere}}



## 100,000 Vistors

With all these customers, you have now got some competition in the market. Your 
boss decides that what our customers really want is the ability to change the choose
the colour of the numbers. Customers, also, want to know the stats for a site, without
having to visit the counter. 

Create a admin page (http://localhost:8080/admin/${{identifier}}) that let's you
choose the colour of the text for the counter. This page should, also, list the referer
urls you are tracking for _identifier_ and display their counts. 

Extra Credit: Allow users to change the color of the text based on the referer.


## 1,000,000 Vistors

You have really hit it big. And you one server can not handle the load, operations 
tried running two servers, but the counts on each server was different. Customers
were unhappy with this. Being resourceful as ever they solved the problem, by 
putting an apache proxy in front of our servers and routed traffic based on the _identifier_
this solved the problem some what. Now our cost have gone up and our hardware utilization 
is all over the place. You system architect has decided that best way to build the system
is to use redis to store the counters, and then have each server retrieve the value and 
generate the count, and increment the value in the redis memory store. Implement
this new feature to allow us to scale our service.

Note: Don't forget about the colour schema.
