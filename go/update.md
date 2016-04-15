# Don't forget to `go get -u`

##### Source: `pain and suffering (large edition)`

Gah. When you use go, you usually pull in new packages something like this `go get -u github.com/someone/somepackage`, and that -u makes Go get that package, and update any packages it references that you might already have. Yay! We can call this point **A**.

So then you might use that for a while -- months, even -- and have it work nicely. Then, you might start to deploy, maybe in a Docker container. Purely hypothetically, of course. And that container might be built from a Dockerfile. Let's call that point **B**, although naughtier letters would be more appropriate.

Trouble is, in between points A and B, some package might have changed in a way that made it not work with some other package, but in a way that fails silently. And that would be a very, very bad thing indeed. It might take you, I don't know, well over a day to hunt that down and figure it out. Truth is, it still might be hard to fix but even harder if you can't replicate it locally.

And before you say "That would have been the first thing to consider, because what else would be different between dev and deploy on docker" I would say, good point, but if the problem was CORS related you can imagine it might no longer be so obvious. You might think of lots of reasons why the staging machine was handling CORS differently than dev, which basically isn't very CORSy at all.

Anyway, there you go.