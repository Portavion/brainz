## **What are the two professional/career highlights you’re most proud of? Why?**
### Stream of consciousness
#### Monaco Masterplan
I have led a masterplan project for the Monaco. The goal was to redesign circulation system in the Principality in order to regain space for pedestrian and vegetation as the city is currently heavily car based with very narrow pedestrian realm. This was a very challenging exercise which required a lot of out of the box thinking. We ended re-designing the road network to be mostly one-way around Monaco whilst keeping select key two way street to act as bypass reducing travel times in case of missed turn and avoiding congestion. This should provide a lot of gained space from the extra traffic lane in places were sidewalk could barely fit two people side by side whilst providing space for planting trees, sitting areas, pocket park, public installations additional greenland.

This was also one of my first experience in remote / asynchronous working as the project combined teams from our uk, canadian and spanish office whilst working alongside Monaco government and the french architects. This forced us to adopt a mostly asynchronous way of working and as been a freeing experience. Holding a very limited amount of online meetings led us to saved a lot of project work time which allowed us to explore schemes in more details. This helped us explore bolder options like the one way system by backing it with basic traffic modelling. Which probably would not have been cost feasible if not for the savings from large regular company wide progress meetings. 

While stressful at first this turned out to be one of the most pleasant way of working I've experienced whilst also aligning with my values of improving sustainable travel methods sustainability etc.
#### Building a suite of python scripts to speed up Gatwick model development and add functionality
Bypassing the VBA interface of the software and using the newer, less document python interface. Allowed to radically speed up the processing of origin/destination matrices. We were working on a large scale 24 hours model which used over 2,000 matrices. While the com interface work well in most cases this was too much for this use case and importing matrices through the COM interface was taking over 3 hours. 

Bypassing excel and processing / importing data through python reduced that process to just under 5 minutes. Took a few different step of optimisation (disable software UI updates, optimise order of import) But this allowed us to save a lot of time in the validation and calibration process, do more runs, which allowed us to deliver a much higher quality model. Ie with the time saving from the old import method we couid do an additional calibration run.
I've also built a few additional scripts that added new functionality to the software that were needed in the context of this project. When designing the parking and drop-off area we were looking at providing the right amount of spaces. Which was difficult given the technical limitations of the software. I've built a script that tracks vehicles going through the airport and forces them to recirculate / loop around if they were not able to find a free space (not allowed in the software) which allowed us to visualise the impact of re-circulation which turned out to be a significant issue in one of the peak hour and led us to provide additional parking space, avoid potential unecessary congestion. 
Finally, I wrote a script that allows to interface a wider corridor model (the two airport and highway system in between) and smaller airport terminal models. This allowed to take travel demand from the wider model (with dynamic vehicle routing and path choice) and convert it to static demand for our more detailed airport model. This allowed to reduce the time it took from the otherwise manual process and avoid a lot of user input error which can be hard to track and correct given the large amout of data.

### Draft
I'm really proud of two projects in particular. Mostly because they either aligned with my values or pushed me creatively to find new ways to solve problems. 

Monaco Masterplan: Rethinking the principality circulation

I led a really ambitious masterplan project for Monaco. The challenge was to redesign the Principality's circulation system which is currently very car-centric to make it a more pedestrian friendly environment. Monaco's streets are very narrow, with hardly any space for pedestrians or greenery. The local government wanted to find ways to reclaim some of that space.

We came up with a mostly one-way system around Monaco, with a few key two-way streets to act as bypass. Whilst a big change, this would allow to free entire traffic lanes in some areas. Going from sidewalks where two people could barely cross each other to having space for wider walkways, trees, seating areas, pocket parks and public art.

This project was also an experiment in asynchronous, remote work. We had teams in the UK, Canada, and Spain working with the Monaco government and French architects. It forced us to be more efficient with communication. Weekly progress meetings were impossible. Cutting down on these freed up a lot of time while not impacting the progress of the project. The extra time let us explore bolder ideas like the one-way system, and back them up with quick traffic modelling. Which would not have been possible without the budget savings from the large company wide progress meetings. The idea was stressful at first, but it ended up being one of the most rewarding and sustainable ways I've worked.

Gatwick Airport Modelling

For a large VISSIM microsimulation modelling project for London's Gatwick airport, I helped remove a big bottleneck in our model development process. We were building 3 big 24-hour model with over 2,000 origin/destination matrices each. The software import tool is built with an Excel-VBA COM interface which works for most case but is not really meant for projects pushing the limits of the software like this one. The software's built-in interface was extremely slow and importing the matrices took over 3 hours.

I felt that excel might be the cause of the bottleneck and used Python to rebuild the COM interface import method by leveraging the software's less documented Python API. I optimised the process in a few steps, like disabling UI updates and optimising the way matrices are batched imported and assigned to vehicle types. This managed to bring down the process to under 10 minutes. This allowed us to do a lot more runs for our calibration and validation process, improving accuracy. Ultimately delivering a much higher-quality base model. 

I also used Python to add  new functionality to the software. We needed to model vehicles recirculating if they couldn't find parking, which VISSIM cannot do natively. I built a script that tracked vehicles and forced them to loop around the network, letting us visualise the impact of recirculation. This showed a congestion issue in one of the peak hours, leading us to recommend additional parking spaces.

Finally, I wrote a script to connected the large-scale corridor model (which covers the two terminals as well as the highway system) with  the smaller, more detailed north and south terminal models. This automated a previously manual process, saving a bit of time but most importantly eliminating potential human entry error which were hard to track amongst the vast amount of data.

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
### **What makes you the best fit for this role?**
I think my excellent background in data analysis, with my ability to pick things up quickly and receive / act on feedback, make me the greatest candidate for this role.

I taught myself web development, including JavaScript, React, Node.js, and database technologies, demonstrating my ability to quickly get and apply new skills. 

Second, I have extensive experience in data analysis through transport modelling. This equipped me with an eye for detail and good problem-solving skills. I'm adept at identifying patterns, troubleshooting issues, and ensuring data accuracy, which are essential for building reliable and robust applications.

Finally, my personal projects showcase my ability to work across the stack. I've successfully implemented front-end interfaces, designed back-end APIs, and managed databases, showing practical experience in building complete web applications. Feel free to have a look through the github repos. I'd be happy to discuss those projects in more details. (https://github.com/Portavion/Chalkr and https://github.com/Portavion/velock)

I'm confident that my ability to learn quickly and my analytical mindset make me an ideal candidate to contribute to Supercritical and thrive in a dynamic environment.

