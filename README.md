# car-path-planning

The model is built in the following way:
1. Build the correct trajectory for both keep lane and change lane scenarios:
    1.1. Check for cars around (in every lane). Pay special attention to the cars in our lane which are in front of us to be able to react (main.cpp, lines 282-320).
    1.2. If there's a car in front of our car driving slow, the first thing to do is to start slowing down and to see if it's reasonable to change lane (safe driving in current lane is covered in: main.cpp, lines 492-497).
    1.3. In order to have the smooth trajectory we use the spline library in the following way: take 2 last points of the trajectory as the car reference points, then add evenly spaced points ahead of the reference points in Frenet coordinates which then will be used for spline approximation; we'll use spline to find out the exact x, y position where we expect our car to be and then build the x, y points based on this. In additon every time we generate the trajectory we are taking into account up to 50 previous points to have the trajectory smooth. The trajectory generation case is covered in main.cpp, lines 411-517
2. Decide whether to keep lane or to change one (the following logic is covered in main.cpp, lines 322-407):
    2.1. If there's a car in front of us driving slow, the car will first check the left lane if there're any surrounding vehicles, if it's safe (see main.cpp, lines 167-186), the car will decide to change the lane, if not - check the right lane if it exists, if it's safe - change the lane, if not - keep the current lane.
    2.2. If the car is driving not in the middle lane, check if it's reasonable (if the traffic goes fast enough and it's safe to do so) to move to the middle lane, if not, keep the current lane.