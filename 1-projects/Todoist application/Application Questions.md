## **What are the two professional/career highlights you’re most proud of? Why?**
### Building the carbon reduction dashboard (align with my values, challenging, interaction with other teams)

### Building python scripts to speed up the matrix input in Gatwick model
Bypassing the VBA interface of the software and using the newer, less document python interface. Allowed to radically speed up the processing of origin/destination matrices. We were working on a large scale 24 hours model which used over 2,000 matrices. While the com interface work well in most cases this was too much for this use case and importing matrices through the COM interface was taking over 3 hours. 

Bypassing excel and processing / importing data through python reduced that process to just under 5 minutes. Took a few different step of optimisation (disable software UI updates, optimise order of import) But this allowed us to save a lot of time in the validation and calibration process, do more runs, which allowed us to deliver a much higher quality model. Ie with the time saving from the old import method we couid do an additional calibration run.
I've also built a few additional scripts that added new functionality to the software that were needed in the context of this project. When designing the parking and drop-off area we were looking at providing the right amount of spaces. Which was difficult given the technical limitations of the software. I've built a script that tracks vehicles going through the airport and forces them to recirculate / loop around if they were not able to find a free space (not allowed in the software) which allowed us to visualise the impact of re-circulation which turned out  and led us to provide additional parking space, avoid potential unecessary congestion.

## **What’s one technical skill, not mentioned in the job ad, that you consider yourself to be very strong in? How would you use it at Doist?**
### Draft
A core technical skill I think I'm strong in is abstraction and conceptual modelling. It is something I have gotten good at through transport modelling. Transport modelling is all about creating a simplified, but still accurate, representation of the real road network. Basically breaking down the road network into smaller components while also figuring their parameters and how they interact together. Things like key junctions, traffic signal timings or even the turning radius of a movement.

I believe this ability to abstract and model complex systems is crucial in programming when designing a new feature, or even more when refactoring existing code. I can use this conceptual modelling skill to break problems down into smaller, more manageable parts. This helps linking smaller components to the bigger picture and design solutions that are both elegant and efficient. I find it really makes it easier to see where things might go wrong and, ultimately, make sure everything works together the way it should.
## **Can you please share links to projects that you're proud of? These could include apps, portfolios, a GitHub profile and/or anything else that showcases your best work. (optional/can be replaced)**

### Draft
I'm really excited by the idea of using tech to solve everyday problems (especially my owns). Here are a couple of side projects that I think showcase this: 

First an iOS climbing app called Chalkr which I am currently working on. 
GitHub: [https://github.com/Portavion/Chalkr](https://github.com/Portavion/Chalkr)

I recently got into bouldering and I'm also a bit of a data geek. I love digging into stats to see how I can improve. I noticed most climbing apps were pretty basic when it came to real training insights when you compared to other apps like Strava or Garmin for running. I wanted something similar, that would let me see what I was doing in my climbing sessions and how my skills are improving. The app lets you easily log every climb – you can even snap a picture of the route and add all the relevant stats.  It tracks how long you're actually climbing on the wall versus resting.Which confirmed I was really bad at taking proper rests... It shows you how you ramp up the difficulty during a session. This helps me make sure I'm warming up properly and not jumping on hard stuff too soon and other useful stats. The app is local first as I wanted to be able to use it while climbing outside with limited signal. I'm currently working on the backend for sync and building a few more useful charts and stats.

I've used React Native and Expo, which was a great way to build for iOS  and continue to develop my React skills. I got to play around with creating custom components to display the data in a way that made sense for climbers. One key technical challenge was figuring out how to efficiently store and retrieve image data,keeping the UI feel smooth even with lots of route photos. I solved it by experimenting with expo image preloading and caching as well as generating a lower resolution thumbnail for each route picture. Which makes loading all route settings almost instantaneous.

Then, there is a quick web app, Velock, which I've built to quickly check the availability of several Santander Bike docking stations.
GitHub: https://github.com/Portavion/velock (which also has a quick demo)

I use the Santander Cycles in London all the time, but I was a little frustrated with their app. You can save favorite stations, but you can't organise them into different lists. And trying to search for a station by address was often a failure as I think they rely on the street road attached to the name of the docking station.

The app lets you create custom lists of stations – I have one for "Home," "Work," "Gym," etc. Makes it super quick to check availability. For the search I used a combination of OpenStreetMap's geocoding API and PostGIS, a spatial extension for PostgreSQL. Which gives more accurate results than the official app. It pulls real-time bike availability data from the TfL Open API. I've built it using Nodejs and Express for the backend with a PostgreSQL database. The frontend is built with React. It was fun getting to work with multiple APIs and integrate them into a single app. TfL Open API has an endpoint to search for docking stations but this only allows match on the station name, like the Santader app. An interesting challenge was implementing a better search feature. I've solved this by getting the coordinates of the input address using OpenStreetMap geocoding endpoint. Then leveraging PostGIS to calculate the shortest distance to each docking stations.

I hope you find these projects as interesting as I found building them and I would love to discuss them further if you were interested.
