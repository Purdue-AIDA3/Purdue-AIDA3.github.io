# 3D Path Planning With Weather Forecasts, Ground Risks, and Airspace Information for UAV Mid-Mile Delivery

## 1 Overview
This work has been submitted to the 2025 American Institute of Aeronautics and Astronautics (AIAA) SciTech conference.

Unmanned aerial vehicles (UAVs) have received immense attention and popularity in recent years. With nearly 400,000 commercial UAVs registered with the Federal Aviation Administration (FAA), it is the fastest-growing segment of aviation in the United States [1].

Since UAVs can function as aerial mobile terminals within wireless/cellular networks, they are widely used in different industries to not only increase efficiency but also to protect humans from hazardous tasks [2]. For instance, a wide range of UAVs have been designed for precision agriculture [3], 3D mapping [4], search and rescue [5], and logistics [6]. Among them, logistics stands out, and large companies such as Amazon, DHL, and FedEx have invested in and researched the feasibility of incorporating UAVs into their commercial services
[7–10]. Most companies focus on last-mile delivery where parcels are delivered directly from fulfillment centers to the delivery address. Mid-mile delivery, on the other hand, focuses on delivering cargo from one fulfillment center to another [11]. Despite the differences, 3D path planning that aims to find the most optimal path under certain costs and constraints must be conducted automatically in order to fully exploit the benefits that UAVs can bring to logistics.

Compared to UAVs for last-mile delivery, which are mostly quadcopters and hexacopters
[10], UAVs for mid-mile delivery are mostly fixed-wings and they are designed very differently.

1 Firstly, UAVs for mid-mile delivery are exposed to more weather conditions due to the longer range of their missions, and weather has a huge impact on both the efficiency and safety as it accounts for or contributes to 35% of fatal general aviation accidents [12]. In general, weather has three main factors (wind, temperature, humidity) to consider for UAVs [13].

For wind, constant wind affects the UAV's ground speed, which is closely related to the fuel consumption and mission complete time, and turbulent flow could causes instability on UAV
states, which affects the cargo and onboard devices [14]. Temperature and humidity are related to icing, turbulence, and thunderstorm [15]. Secondly, UAVs for mid-mile delivery are much larger than most UAVs and they fly at relatively low altitudes. Therefore, there is little time to react when loss of control happens and the consequence of it is catastrophic. Lastly, since UAVs do not have pilots onboard, when they are flying beyond visual line of sight, they may be restricted to only fly in certain airspaces and avoid crowded air traffic.

The above mentioned challenges are unique to UAVs for mid-mile delivery and must be taken into account in the 3D path planning algorithm. In this paper, we aim to find the optimal 3D path for the UAV mid-mile delivery under costs and constraints that are constructed from the weather forecasts, ground risks, and airspace information. The weather forecasts are obtained from the national weather service which provides high resolution gridded weather forecast data at different flight levels. The ground risks are computed based on the population density. The airspace information can obtained from publicly accessible places such as SkyVector. To the best of our knowledge, there are few works in the UAV 3D
path planning literature that formulates the problem with all the aforementioned information for UAV mid-mile delivery. In the end, the optimal 3D path planning problem is solved with several evolution algorithms and a performance comparison is provided.

## 2 Related Works

UAV 3D path planning, finding the optimal 3D path for UAVs to reach certain destinations, is one of the most important problems to solve in order to fully utilize the advantages of UAVs [10]. It is proven that an optimal solution for such problem is NP-complete, that is, no polynomial time solution is known to exist, if it is searched in an exhausting way [16].

Therefore, a tremendous amount of research has been done. In general, the approaches for UAV path planning can be grouped into five main categories: classical, heuristic, metaheuristic, machine learning-based, and hybrid approaches [17]. Meta-heuristic approaches receive an increased amount of attention in recent years due to its robustness, adaptability, and effectiveness, and they can be further divided into swarm intelligence and evolutionary algorithms [18,19]. Due to the sheer amount of works published in this domain, it is difficult, if not impossible, to provide an extensive review. Therefore, this paper only reviews works that are closely related to this paper. Interested readers may find the cited survey papers helpful [17–19].

Zheng et. al is one of the first groups that applied the genetic algorithm (GA), the most classical evolutionary algorithm, to the 3D path planning for UAVs [20]. In [20], the UAV's states such as maximum turning angle and maximum climbing/diving angle are considered, and the generated path is optimal in terms of the length of each line segment, average altitude above the sea level, and avoiding certain ground sites. It is demonstrated that GA can effectively find the optimal path for not only a single UAV, but also a group of UAVs under multiple nonlinear constraints. Bao et. al applied the particle swarm optimization (PSO), the most classical swarm intelligence algorithm, to find the shortest path for the reconnaissance mission in a 2D environment [21]. Both GA and PSO are popular meta-heuristic approaches and many variants have been proposed [18]. In [22], Roberge et. al did a thorough comparison between GA and PSO in multiple complex 3D scenarios. Compared to authors of previous works, Roberge et. al additionally considered the power and fuel consumption of the UAV and the simulation results showed that GA outperformed PSO in most scenarios. The same group also utilized the GPU's parallel computation to greatly accelerate GA and achieved a speedup of 290 times compared to solely using CPU [23], allowing GA to be utilized for in-flight replanning. More recently, Yu et. al applied four variants of the differential evolution (DE), another evolutionary algorithm, to 3D path planning and found their proposed constraint differential evolution algorithm outperforms those variants [24].

The above mentioned works mainly focus on using UAV states and restricted areas as the constraints, which are also important for 3D path planning for mid-mile delivery UAVs. However, as discussed in Section 2, severe weather conditions and ground risks are also critical to mid-mile delivery UAVs, but most works that consider meteorological factors focus on 3D
path planning of solar-powered UAVs where wind and solar radiation play the main roles [25–27]. Duan et. al utilized the weather forecasts to compute the icing index, Richardson number, which is related to turbulence and thunderstorm, and wind speed to generate the path with the least amount of travel time for a long-range UAV [28]. However, the authors did not consider limits on the UAV states and restricted areas, and the generated path is in 2D. Su et. al and Hu et. al proposed novel frameworks for assessing risks that UAVs can cause to the ground in rural and urban environment, respectively [29, 30]. A comprehensive review of unmanned aircraft system ground risk models can be found in [31]. However, most works did not incorporate the risk assessment into a 3D path planning problem. This paper aims to fill the research gap by integrating weather forecast, ground risk, and airspace information into the 3D path planning problem for UAV mid-mile delivery.


## References

[1] Federal Aviation Administration, "Drone safety day." https://www.faa.gov/uas/
events/drone_safety_day, April 2024. (Accessed: May 6, 2024).

[2] M. Ghamari, P. Rangel, M. Mehrubeoglu, G. S. Tewolde, and R. S. Sherratt, "Unmanned aerial vehicle communications for civil applications: A review," *IEEE Access*,
vol. 10, pp. 102492–102531, 2022.

[3] P. Radoglou-Grammatikis, P. Sarigiannidis, T. Lagkas, and I. Moscholios, "A compilation of uav applications for precision agriculture," *Computer Networks*, vol. 172, p. 107148, 2020.

[4] F. Nex and F. Remondino, "Uav for 3d mapping applications: a review," *Applied Geomatics*, vol. 6, pp. 1–15, 2014.

[5] M. Lyu, Y. Zhao, C. Huang, and H. Huang, "Unmanned aerial vehicles for search and rescue: A survey," *Remote Sensing*, vol. 15, no. 13, 2023.

[6] X. Li, J. Tupayachi, A. Sharmin, and M. Martinez Ferguson, "Drone-aided delivery methods, challenge, and the future: A methodological review," *Drones*, vol. 7, no. 3, 2023.

[7] Amazon, "Amazon drone delivery is coming to arizona." https://www.aboutamazon.

com/news/transportation/amazon-drone-delivery-arizona, April 2024. (Accessed: May 6, 2024).

[8] DHL, "Drones." https://www.dhl.com/us-en/home/insights-and-innovation/
thought-leadership/trend-reports/drones-logistics.html, 2024. (Accessed:
May 6, 2024).

[9] FedEx, "Fedex plans to test autonomous drone cargo delivery with elroy air." https:
//newsroom.fedex.com/newsroom/global/elroyair, March 2022. (Accessed: May 6, 2024).

[10] A. Thibbotuwawa, G. Bocewicz, P. Nielsen, and Z. Banaszak, "Unmanned aerial vehicle routing problems: A literature review," *Applied Sciences*, vol. 10, no. 13, 2020.

[11] N. Gunady, S. Vashi, B. Kim, H. Chao, D. A. DeLaurentis, and W. A. Crossley, "Exploring middle mile cargo operations with urban air mobility across metro areas," in AIAA AVIATION 2023 Forum, 2023.

[12] A. J. Fultz and W. S. Ashley, "Fatal weather-related general aviation accidents in the united states," *Physical Geography*, vol. 37, no. 5, pp. 291–312, 2016.

[13] Y. Averyanova and E. Znakovskaja, "Weather hazards analysis for small uass durability enhancement," in 2021 IEEE 6th International Conference on Actual Problems of Unmanned Aerial Vehicles Development (APUAVD), pp. 41–44, 2021.

[14] B. H. Wang, D. B. Wang, Z. A. Ali, B. T. Ting, and H. Wang, "An overview of various kinds of wind effects on unmanned aerial vehicle," *Measurement and Control*, vol. 52, no. 7-8, pp. 731–739, 2019.

[15] B. C. Bernstein, F. McDonough, M. K. Politovich, B. G. Brown, T. P. Ratvasky, D. R.

Miller, C. A. Wolff, and G. Cunning, "Current icing potential: Algorithm description and comparison with aircraft observations," *Journal of Applied Meteorology*, vol. 44, no. 7, pp. 969 - 986, 2005.

[16] R. Szczerba, "Threat netting for real-time, intelligent route planners," in *1999 Information, Decision and Control. Data and Information Fusion Symposium, Signal Processing* and Communications Symposium and Decision and Control Symposium. Proceedings
(Cat. No.99EX251), pp. 377–382, 1999.

[17] Amylia Ait Saadi, Assia Soukane, Yassine Meraihi, Asma Benmessaoud Gabis, Seyedali Mirjalili, and Amar Ramdane-Cherif, "Uav path planning using optimization approaches: A survey," *Archives of Computational Methods in Engineering*, vol. 29, no. 6, pp. 4233–4284, 2022.

[18] S. Poudel, M. Y. Arafat, and S. Moh, "Bio-inspired optimization-based path planning algorithms in unmanned aerial vehicles: A survey," *Sensors*, vol. 23, no. 6, 2023.

[19] Y. Zhao, Z. Zheng, and Y. Liu, "Survey on computational-intelligence-based uav path planning," *Knowledge-Based Systems*, vol. 158, pp. 54–64, 2018.

[20] C. Zheng, L. Li, F. Xu, F. Sun, and M. Ding, "Evolutionary route planner for unmanned air vehicles," *IEEE Transactions on Robotics*, vol. 21, no. 4, pp. 609–620, 2005.

[21] Y. Bao, X. Fu, and X. Gao, "Path planning for reconnaissance uav based on particle swarm optimization," in 2010 Second International Conference on Computational Intelligence and Natural Computing, vol. 2, pp. 28–32, 2010.

[22] V. Roberge, M. Tarbouchi, and G. Labonte, "Comparison of parallel genetic algorithm and particle swarm optimization for real-time uav path planning," *IEEE Transactions* on Industrial Informatics, vol. 9, no. 1, pp. 132–141, 2013.

[23] V. Roberge, M. Tarbouchi, and G. Labont´e, "Fast genetic algorithm path planner for fixed-wing military uav using gpu," IEEE Transactions on Aerospace and Electronic Systems, vol. 54, no. 5, pp. 2105–2117, 2018.

[24] X. Yu, C. Li, and J. Zhou, "A constrained differential evolution algorithm to solve uav path planning in disaster scenarios," *Knowledge-Based Systems*, vol. 204, p. 106209, 2020.

[25] L. Wirth, P. Oettershagen, J. Amb¨uhl, and R. Siegwart, "Meteorological path planning using dynamic programming for a solar-powered uav," in *2015 IEEE Aerospace* Conference, pp. 1–11, 2015.

[26] S.-H. Kim, G. E. G. Padilla, K.-J. Kim, and K.-H. Yu, "Flight path planning for a solar powered uav in wind fields using direct collocation," *IEEE Transactions on Aerospace* and Electronic Systems, vol. 56, no. 2, pp. 1094–1105, 2020.

[27] J.-S. Lee and K.-H. Yu, "Optimal path planning of solar-powered uav using gravitational potential energy," *IEEE Transactions on Aerospace and Electronic Systems*, vol. 53, no. 3, pp. 1442–1451, 2017.

[28] C. Duan, J. Feng, and H. Chang, "Meteorology-aware path planning for the uav based on the improved intelligent water drops algorithm," *IEEE Access*, vol. 9, pp. 49844–
49856, 2021.

[29] Y. Su, Y. Xu, and G. Inalhan, "A comprehensive flight plan risk assessment and optimization method considering air and ground risk of uam," in *2022 IEEE/AIAA 41st* Digital Avionics Systems Conference (DASC), pp. 1–10, 2022.

[30] M. Hu, B. Pang, F. Dai, and K. H. Low, "Risk assessment model for uav cost-effective path planning in urban environments," *IEEE Access*, vol. 8, pp. 150162–150173, 2020.

[31] A. Washington, R. A. Clothier, and J. Silva, "A review of unmanned aircraft system ground risk models," *Progress in Aerospace Sciences*, vol. 95, pp. 24–44, 2017.