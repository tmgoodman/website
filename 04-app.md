---
title: Route Assignment Finder Application
subject: 
subtitle: 
short_title: Analysis and Design Document
authors:
  - name: Tegan Goodman
    affiliations:
      - San Diego State University
      - Salt-Free Solutions
    email: tgoodman5670@sdsu.edu
license: 
keywords: app analysis, design 
Introduction: The Route Assignment Finder is a Streamlit-based web application designed to help users select, analyze, and visualize waste collection routes for specific dates. It integrates geospatial analysis, database querying, and interactive mapping features to enhance route management and vehicle tracking. 

kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: docx
  - format: pdf
    template: volcanica
    article_type: Report
---

# Route Assignment Finder Application
# Background Information 
The Environmental Services Department (ESD) is responsible for managing waste collection services in San Diego, including refuse, recycling, and green waste pickup. To improve efficiency and sustainability, the department actively tracks collection routes and vehicle movements using GIS data and GPS technology. ESD records waste tonnage data through two key systems: ARTS, where supervisors manually log load data, and RAD, which collects weight measurements from landfill scales. 

As part of its ongoing efforts to enhance waste management, ESD is implementing route rebalancing under Measure B, a policy change that amends the San Diego Municipal Code to allow the City to charge fees for solid waste services. This transition requires adjustments to collection routes as some properties shift to private service providers. The goal of rebalancing is to optimize routes for safer, more efficient pickups, reducing operational costs, fuel consumption, and vehicle wear while ensuring a balanced workload among drivers. To support this effort, ESD has partnered with Routeware, a company specializing in route optimization technology. 

To maintain data integrity during this transition, ESD developed an app that enables data analysts to monitor collection routes and validate information across multiple systems. The app provides a centralized resource for tracking key metrics, including route paths, driver assignments, truck usage, tonnage collected, and route completion times. By consolidating this information, the tool helps ensure accurate data as the department adjusts and refines its operations under Measure B. 

Beyond data validation, the app also serves as a management tool for monitoring driver performance. By analyzing time spent on routes, supervisors can identify inefficiencies, address potential challenges, and provide support to drivers who may need additional guidance. This data-driven approach enhances operational oversight, enabling ESD to make informed decisions that improve overall service quality. Ultimately, the app plays a critical role in facilitating a smooth transition during the rebalancing process, promoting greater efficiency, accountability, and sustainability in waste collection services. 

# 1.2 Scope 

## In Scope 

Developing a web-based application with an interactive user interface. 

Implementing algorithms for route optimization. 

Ensuring secure user authentication and data protection. 

Providing visualization tools for better route management. 

Allowing users to manually override automated recommendations. 

Generating reports based on route assignments and optimizations. 

## Out of Scope 

Integration with third-party mapping services beyond basic visualization. 

Real-time GPS tracking and live route updates. 

Mobile application development (the initial version is web-based only). 

Advanced AI-based predictive analytics beyond rule-based optimizations. 

Handling logistics and fleet management beyond route assignments. 

 

# 1.3 Assumptions 

The Collection Services Division of the Environmental Services Department of the City of San Diego will provide all operational data, including vehicle data, route information, and any necessary logistical details.  

All spatial data will be regularly updated, accurate, and accessible through reliable systems, ensuring that users have access to the most current data available. 

The application assumes users have a basic understanding of operation and functionality of CSD, including selecting routes and vehicles for analysis. 

All analysis and decision-making will be based on data collected from GPS tracking on trucks and from landfill operations.  

Users must download and install the necessary files or software components required to operate the application, ensuring that the system is fully functional upon use. 

A stable and consistent Wi-Fi connection is required for data retrieval, processing, and communication with the application. 

The software will be compatible with commonly used operating systems, including Windows, macOS, iOS, and Android, and will work across devices without requiring specific hardware configurations. 

Users are expected to have access to and be familiar with the necessary hardware (e.g., computers, tablets, or smartphones) to run the application efficiently. 

# 1.4 Constraints 

The application must operate within the defined date range of August 2024, restricting its functionality to these months for data input, analysis, and reporting. 

The application relies on data from ARTS/RAD, so its accuracy and performance are dependent on the integrity and quality of the data provided by these systems. Any inconsistencies or errors in the source data may affect the application's functionality and outputs. 

Staff availability may impact the project timeline, causing delays in development, testing, deployment, and support. 

The application is locally hosted, meaning it will be managed on internal servers, limiting scalability and flexibility compared to a cloud-based solution. 

The application must comply with the city’s internal data security and privacy policies, which may impose limitations on data sharing, access control, and user authentication. 

User access to the application may be limited by internal IT policies, including permissions, security protocols, or access to specific network resources. 

System performance may be constrained by the local infrastructure, including the local user’s PC... server capacity or hardware restrictions within the hosting environment. 

# 1.5 Dependencies 

GIS data, including routes, vehicles, and landfill info, must be regularly updated to ensure accurate visualizations and reports. 

The application relies on DuckDB for data storage and querying. Any database issues, like downtime or maintenance, could affect functionality and data access. 

User access depends on compatible browsers, network settings, and IT resources. Changes in IT policies could affect access or functionality. 

# 2. Features 

# 2.1 User Interface  

Visual Branding 

Displays images, logos, and other visuals for branding. 

Layout and Input Fields 

Clean, user-friendly layout. 

Input fields for user interactions, with specific areas for:  

Waste commodity selection (dropdown or selection options). 

Route number input (5-digit route number field). 

Date Picker: Restricts user to selecting dates only in August and September 2024. 

Data Visualization 

Clear display of relevant visualizations such as:  

Vehicle counts for selected routes. 

Route maps based on selected commodity types. 

Route-specific data such as missed pickups, population, census data 

For details on the user interface, refer to Appendix 5.2. 

# 2.2 Backend  

Database Connection 

Utilizes DuckDB to connect to and query the data. 

Loads spatial extension for processing geospatial data. 

Data Querying and Processing 

Queries vehicle data from GPS tracking tables. 

## Filters data based on:  

Selected route 

Date range (August and September 2024) 

Vehicle number (5-digit route number). 

Loads shapefiles for route layers, specifically tailored to each commodity type. 

Vehicle Tracking and Analysis 

Queries RAD and ARTS databases for load and material details. 

Displays top vehicle counts for selected routes. 

Allows for vehicle selection based on available data. 

Geospatial Processing 

Converts GPS data into GeoDataFrame format for spatial analysis. 

Performs spatial joins with route and landfill layers. 

Identifies landfill visit times and organizes route tracking:  

Before and after landfill visits. 

Additional Information Display 

Fetches route-specific information such as:  

Missed pickups. 

Population data. 

Census data. 

Conducts spatial joins to assess landfill interactions with routes. 

Error Handling 

Implements exception handling for potential issues like:  

Missing data. 

Index errors. 

Ensures robust processing of timestamped route activities to avoid data inconsistencies. 

 

# 3. Technologies Used 

# 3.1 Integrated Development Environment (IDE) 

An Integrated Development Environment (IDE) is a software application that provides a comprehensive workspace for developers to write, test, and debug code efficiently. IDEs integrate multiple development tools into a single interface, including a code editor, compiler or interpreter, debugger, and project management tools. This setup allows developers to streamline their workflow, reducing context switching and improving productivity. 

## Key features of an IDE include: 

Syntax highlighting – Enhances readability and helps identify errors. 

Code completion – Suggests function names, variables, and syntax elements to speed up coding. 

Integrated debugging – Provides tools to identify and fix errors in real-time. 

Version control support – Allows seamless integration with Git and other version control systems for tracking changes. 

Project navigation – Enables easy management of files and dependencies within a structured workspace. 

For our specific use case, an IDE is essential for developing and maintaining our Streamlit application. It enables efficient debugging, testing, and real-time modification of our Python scripts, ensuring a smooth development process. Given our focus on geospatial analysis and data visualization, an IDE such as Visual Studio Code (VS Code) or PyCharm provides powerful tools to write Python scripts, test GIS libraries like geopandas, and integrate with databases like DuckDB. The use of an IDE allows us to efficiently iterate on our app, add features, and ensure a stable and scalable application. 

# 3.2 Python Environment 

A Python environment refers to the setup that includes the Python interpreter, libraries, and dependencies required to run Python code. Managing Python environments is crucial for maintaining consistency across projects and avoiding dependency conflicts. There are several types of Python environments: 

System-wide Python Installation – Installed globally and used across different projects, but can lead to version conflicts. 

Virtual Environments (venv or virtualenv) – Isolated environments for specific projects, ensuring dependency control. 

Conda Environments – Used in data science workflows, allowing package management for scientific computing. 

Docker/Containerized Environments – Provide reproducibility by encapsulating code, dependencies, and system configurations in a container. 

For our use case, we need a well-structured Python environment to run our Streamlit application and handle geospatial data processing. We will likely use a virtual environment (venv or conda) to manage dependencies, ensuring compatibility with libraries such as pandas, geopandas, streamlit, folium, and duckdb. This setup allows us to keep our development workspace organized and prevents version mismatches between different projects. Additionally, cloud-based environments like Google Colab or Jupyter Notebooks can be useful for preliminary data exploration before integrating findings into our main application. 

# 3.3 Google Earth Engine (GEE) 

Google Earth Engine (GEE) is a cloud-based geospatial analysis platform designed for large-scale environmental monitoring, remote sensing, and spatial data analysis. It provides access to a vast repository of satellite imagery and geospatial datasets, including data from NASA’s Landsat, MODIS, Sentinel, and other global environmental datasets. GEE enables users to analyze trends, detect changes, and build predictive models using JavaScript or Python APIs. 

## How GEE is Useful for Our Project: 

Access to Satellite Imagery – We can use GEE to obtain high-resolution satellite images for analyzing landfills, waste collection zones, and urban infrastructure. 

Geospatial Data Processing – GEE’s cloud-based environment allows efficient raster and vector data analysis without requiring extensive local computational resources. 

Environmental Analysis – We can monitor waste collection efficiency, urban sprawl, and environmental impacts in real time. 

Integration with Python & Streamlit – By using the Python API, we can integrate GEE with our Streamlit dashboard to visualize geospatial insights dynamically. 

 

# 3.4 Streamlit 

Streamlit is an open-source Python framework that simplifies the process of building interactive web applications for data visualization and machine learning models. Unlike traditional web frameworks, Streamlit allows users to turn Python scripts into web apps with minimal effort, eliminating the need for HTML, CSS, or JavaScript. 

## Key Features of Streamlit: 

Real-time interactive widgets – Users can interact with filters, sliders, and maps to explore data dynamically. 

Automatic UI generation – Streamlit automatically renders widgets and graphs based on the Python script, reducing development time. 

Seamless integration with data libraries – Works with Pandas, Matplotlib, Plotly, Folium, and Geopandas for advanced data visualization. 

Live updates and caching – Ensures fast rendering and smooth user experience. 

## How We Use Streamlit in Our Project: 

Visualizing Collection Routes – We can use Streamlit and Folium to display interactive maps of landfill sites, collection zones, and truck routes. 

Analyzing Missed Pickups – Streamlit can generate graphs and tables showing missed collections, allowing supervisors to identify problem areas. 

Comparing Waste Collection Metrics – We can integrate data from GPS tracking, landfill tonnage (RAD), and recycling routes into a single dashboard for analysis. 

Dynamic Filtering – Users can filter by district, waste type, or route ID to explore trends and optimize operations. 

# Conclusion 

Each of these technologies plays a vital role in our project: 

IDE streamlines development and debugging. 

Python environments ensure dependency management and reproducibility. 

Google Earth Engine provides access to powerful geospatial analysis tools. 

Streamlit transforms complex data into an interactive and user-friendly web application. 

By integrating these tools effectively, we create a data-driven waste management system that enhances operational efficiency, optimizes collection routes, and improves environmental sustainability. 

 

 

# 4. Requirements 

# 4.1 Setting up environment 

Open the Telematics Folder in IDE 

Open Terminal: On the taskbar, click on the terminal dropdown and click on New Terminal. 

In the terminal, type the following to create a conda mamba environment: 

conda create -n streamlit_env 

Activate the newly created environment: 

conda activate streamlit_env 

In IDE, go to View > Command Palette > Select Interpreter, and choose the interpreter with ‘streamlit_env’ in the name.  

Run the following command in the terminal to install dependencies: 

pip install streamlit streamlit_folium geopandas duckdb ee geemap 

Create a Google Cloud Account if you don’t already have one. 

Create a New Project in the Google Cloud Console and give it a specific project name. 

In VS Code, go to line 299 of your new_app.py file and update the project name: 

project = '<your project name>'   

Enable the Google Earth Engine API in the Google Cloud Console for your project. 

Register the Project with Google Earth Engine to link it to your project.  

Run the Streamlit app by executing: 

streamlit run new_app.py 

If it doesn’t run, try another port: streamlit run new_app.py --server.port 8080 

4.2 Data 

Ensure your have the following files and folders: 

Files: 

gps.db 

DuckDB database containing several tables: 

ARTS - data manually logged by supervisors such as driver assignment for truck/route  

RAD - data collected from landfill scale such as tonnage measurements 

GPS – records the real-time location and movement of collection trucks, including vehicle details, speed, timestamps, and spatial coordinates 

routes.pqt 

provides information on collection routes, including operational details, infrastructure metrics, and spatial attributes 

new_app.py 

Python script used to run the Streamlit application for data visualization and analysis. 

Logo.png 

Image file of Environmental Services department logo 

pic1.png, pic2.png, pic3.png 

Image files featuring trucks and San Diego logo 

Each shapefile contains attributes such as district, route ID, household count, load capacity, and spatial geometry representing collection areas. 

Landfill – Polygon data representing landfill locations. 

Org – Organics collection routes. 

org_htc – Hard-to-collect organics collection routes. 

Rec – Recycling collection routes. 

rec_htc – Hard-to-collect recycling collection routes. 

Ref – Refuse (trash) collection routes. 

ref_htc – Hard-to-collect refuse collection routes. 

For detailed dataset schemas, refer to Appendix 5.2. 

# 4. Next Steps 

# 4.1 Improvements 

Several enhancements can be made to improve both the functionality and user experience of the application: 

Visual Design: Refine the visual layout to make the application more cohesive, modern, and user-friendly by using consistent color schemes, spacing, and typography. 

Expanded Data Analysis: Incorporate more advanced data analytics, such as historical trends, missed pickup patterns, and predictive insights, rather than focusing solely on basic routing information. 

Increased Interactivity: Add features like filterable metrics, dynamic tooltips, and interactive charts to allow users to explore the data in more detail. 

Enhanced Mapping: Improve the map visualization of truck routes with clearer styling, better labeling, and the ability to view specific days, neighborhoods, or truck IDs. 

Real-Time Data Integration: Incorporate live data feeds (e.g., from GPS tracking or RAD systems) to reflect real-time truck locations, container fill levels, or active service requests. 

These improvements would significantly enhance the value and usability of the application for decision-makers and field supervisors. 

# 4.2 Future Work 

Currently, the application is hosted on Streamlit, which is ideal for development and internal testing. However, to support wider access and real-world deployment, we can explore more robust hosting options: 

Cloud Deployment: Hosting the application on platforms such as AWS (Amazon Web Services), Google Cloud Platform, or Microsoft Azure would allow us to scale the app for larger user bases and ensure high availability. These platforms also offer built-in security, load balancing, and database integration. 

Containerization with Docker: Packaging the application in a Docker container would make it portable and easier to deploy across different environments, whether locally or in the cloud. This also improves consistency across development, testing, and production stages. 

Integration with City Infrastructure: For long-term use, the application could be embedded into existing internal portals or dashboards used by city departments, allowing seamless access for supervisors and analysts. 

API Development: Creating APIs to connect with real-time data sources (e.g., GPS databases, RAD systems, service request platforms) would enable continuous data updates and improve interactivity. 

User Management and Authentication: To support multiple users with different access levels (e.g., field staff vs. administrators), we can implement user authentication and role-based access control. 

These steps would help move the application from a prototype to a fully operational tool that can be used across departments and adapted for broader public service applications. 

# 5. Literature Review 

# 5.1 Analysis and Design Document – Route Optimization Solution Integration (CGI) 

The Analysis and Design Document – Route Optimization Soultion Integration is a formally structured technical deliverable by CGI that outlines the integration of Routeware's route optimization system with the Environmental Services Department's (ESD) GIS environment. The document is organized into major sections and appendices, each serving a specific function within the software development and deployment lifecycle. Below is a detailed review focused on its section headings, content scope, and formatting approach: 

## 1. Preliminary Analysis 

This foundational section provides the context, scope, and constraints for the project. 

## 1.1 Overview 
Introduces the operational need for integrating Routeware with ESD’s GIS, driven by inefficiencies in current manual processes and regulatory expansion (e.g., Organics collection). It describes system architecture and integration goals, using clear and actionable language. 

## 1.2 Assumptions 
Lists project constraints such as API-based data transfers, consistent primary keys, and staffing availability for UAT and deployment validation. This section adheres to standard systems design practices by identifying preconditions for success. 

## 1.3 Constraints 
Outlines known limitations like environment availability and vendor staff timing, linking these to potential project delays. 

## 1.4 Dependencies  
Identifies critical system infrastructure (e.g., GISAPPSERVERDEV, ATLASQA) and software versioning (ArcGIS 10.8.1). This addition makes the project’s technical foundation clearer and more auditable. 

## 2. Business Process 

This section defines business-level requirements from a functional and organizational perspective. 

## 2.1 High-Level Business Requirements – Presented in a tabular format with columns for Req#, Requirement, Comments, and Priority, allowing traceability and prioritization.  

## 3. Quality Assurance 

A brief but essential section covering testing responsibilities and phases, divided between CGI and client roles. It outlines acceptance standards, indicating the collaborative QA process used for deployment validation. 

## 4. Effort Estimate 

This section presents resource and cost modeling, structured into three subsections: 

4.1 Total GIS Integration Effort by Feature – Lists tasks (e.g., Dev Consultation, Hypercare Support) with hour estimates and priority comments. This enables effective budgeting and workload distribution. 

4.2 Total Project Management Effort – Identifies 635 hours allocated to full-lifecycle PM, including Hypercare, and notes post-Hypercare disengagement dates. This precision supports contractual planning. 

4.3 Total Cost by Role – Although not fully visible in the provided content, this section likely completes the financial model with per-role cost allocations, a standard inclusion in technical project plans. 

## 5. Project Timeline 

A planning section that visually defines the sequence of deliverables across phases, including UAT and deployment for each. This supports risk mitigation and alignment with organizational rollouts. 

## 6. Appendices 

The appendices provide critical technical artifacts and schema details to support implementation. 

## 7.  Formatting 

The document is consistently formatted with: 

Numbered section headings for navigation and version control. 

Clear use of tables for requirements, assumptions, and effort estimates. 

Use of diagrams and appendices to visually support text-heavy sections. 

Progressive updates tracked in the Revision History, indicating structured document lifecycle management. 

# 5.2 The Design and Implementation of a Garbage Truck Fleet Management System 

The design and implementation of a garbage truck fleet management system is a research article focused on the design and implementation of a Garbage Truck Fleet Management System (GTFMS) that integrates arrival time forecasting and an optimized power-saving mechanism for mobile applications. The study highlights how advances in cloud computing, mobile computing, and intelligent transportation systems (ITS) can be applied to improve urban waste collection services. This review outlines the structure of the original article, describes the main topics covered in each section, and includes notes on formatting such as the use of figures, graphs, and mathematical models. 

## 1. Abstract 

Summarizes the scope, methodology, and key findings of the study. 

Introduces the GTFMS architecture and highlights power efficiency and forecasting accuracy. 

## 2. Introduction 

Discusses the context of ITS and mobile apps in public services. 

Establishes the motivation for developing a garbage truck app with real-time and predictive features. 

Briefly mentions forecasting methods and concerns about power usage. 

## 3. Literature Review 

Divided into three subsections: 

## 3.1 Message Updating Mechanism 

Reviews studies on optimizing update frequency and reducing power consumption. 

## 3.2 Arrival Time Forecasting Method 

Summarizes machine learning techniques such as regression, k-NN, SVM, and neural networks used for travel time prediction. 

## 3.3 Cloud Computing 

Explains the role of distributed computing in managing large datasets for real –time services. 

## 4.  Design of Management System 

Describes the system’s three components: On-Board Units (OBUs), Fleet Management System(FMS), and Geographic Tracking Application (GTA). 

## 5. Model Optimization and User Feedback 

Presents a six-step process based on user location and garbage truck proximity. 

## 5.1 Arrival Time Forecasting Method 

Details the use of weighted multiple linear regression models and training procedures. 

## 5.2 Message Updating Mechanism 

Describes how and when updates are triggered based on user settings and historical averages. 

## 5.3 Case Study and Availability Rate Analysis 

Includes a case study from Hsinchu City and performance metrics. 

## 5.4 Cloud Computing for Forecasting 

Explains how the system uses Hadoop and MapReduce to scale the forecasting process. 
 

## 6. Implementation and Evaluation 

## 6.1 Implementation: Describes the deployment of the app on an Android device and how it interacts with user preferences. 

## 6.2 Evaluation: Analyzes forecasting accuracy using historical route data collected over sevenmonths. 

## 7. Conclusion and Future Work 

Summarizes the effectiveness of the proposed system in improving prediction accuracy and energy efficiency. 

Suggests areas for future enhancement, such as expanded datasets or algorithm refinements. 

## 8. Formatting 

Use of Figures and Graphs  

Mathematical Models  

Consistent font, no color in the text 

Numbered headers. 

Reference Section  

 
# 5.3 Application for Image Recognition in Waste Management 

RecycleMate is a mobile application designed to help users identify recyclable items and locate nearby recycling facilities using image recognition and geolocation. 

## 1. Abstract 

Summarizes the scope and key findings of image recognition in recycling systems. 

Highlights the use of machine learning, particularly convolutional neural networks (CNNs), to classify recyclable materials. 

Emphasizes real-time classification accuracy and mobile integration. 

## 2. Introduction 

Discusses the global challenge of improper waste sorting and declining recycling rates. 

Establishes the motivation for developing AI-powered tools to help individuals and municipalities sort waste accurately. 

Introduces image recognition as a scalable solution for public awareness and operational efficiency. 

## 3. Literature Review 

Divided into three subsections: 

## 3.1 Image Classification Models 

Reviews common machine learning models used for image classification: CNNs, MobileNet, ResNet, and custom-trained AutoML Vision models. 

Discusses training datasets such as TrashNet, TACO (Trash Annotations in Context), and proprietary datasets. 

Emphasizes tradeoffs between model complexity and mobile deployment. 

## 3.2 Mobile and Web Applications 

Summarizes several mobile applications, such as RecycleMate and Lasso, that allow users to scan waste items. 

Highlights UI/UX considerations for real-time interaction. 

Notes challenges in lighting conditions, image clarity, and model interpretability. 

## 3.3 Integration with Recycling Infrastructure 

Discusses how systems can be integrated into Material Recovery Facilities (MRFs) or smart bins. 

Outlines potential for automated sorting arms or robotic mechanisms. 

Mentions pilot studies in urban cities exploring image-assisted bin classification. 

## 4. Design of Image Recognition System 

Describes a modular design comprising: 

Mobile application (user-facing front-end). 

Cloud-based classification service (e.g., Google AutoML, AWS Rekognition). 

Optional feedback module for model retraining. 

Notes asynchronous processing to minimize app delay. 

## 5. Model Optimization and User Feedback 

## 5.1 Data Augmentation and Preprocessing 

Details common techniques: rotation, background removal, contrast enhancement. 

Notes importance of representative data for training and evaluation. 

## 5.2 Active Learning and Retraining 

Describes how user corrections can be used to retrain models periodically. 

Encourages a feedback loop between users and developers. 

## 5.3 Performance Metrics 

Reports classification accuracy between 85–95% depending on the dataset and model. 

Includes precision-recall analysis and confusion matrix for common material types (plastic, glass, paper, etc.). 

## 5.4 Scalability in the Cloud 

Explains how services like Google Cloud Vision or AWS Lambda scale to handle multiple concurrent requests. 

Discusses latency reduction strategies and cost tradeoffs. 

## 6. Implementation and Evaluation 

## 6.1 Implementation: 

Describes deployment on Android and iOS using cross-platform tools like React Native or Flutter. 

Notes integration with image APIs, real-time feedback, and camera handling. 

## 6.2 Evaluation: 

Evaluates the model with a test set and real-world user trials. 

Discusses user engagement data, error rates, and usability surveys. 

## 7. Conclusions and Future Work 

Concludes that image recognition significantly enhances user participation and accuracy in recycling. 

Recommends future work in: 

Expanding to more item types. 

Improving edge-device processing. 

Integrating with location services to offer disposal sites. 

Exploring multilingual or voice-based interfaces. 

## 7. Relationship to Our Work 

While RecycleMate focuses on individual user education and behavior change, our project targets municipal-level operational efficiency. 

## Shared goals: 

Both aim to improve waste management systems through technology-driven solutions. 

Both emphasize location-based services, with RecycleMate using geolocation to find facilities, and Route Assignment Finder leveraging geospatial data for route analysis. 

## Key differences: 

RecycleMate uses computer vision (image recognition) to classify waste items, while Route Assignment Finder uses spatial joins and routing algorithms for logistical planning. 

RecycleMate is citizen-facing, promoting recycling awareness, while Route Assignment Finder is staff-facing, enhancing service delivery operations. 

## Potential integration: 

Data from RecycleMate (e.g., recycling drop-off demand hotspots) could inform route planning in Route Assignment Finder. 

Our project could expand to include interactive tools for public education, similar to RecycleMate, using dashboard elements. 

# Analysis and Design Document
:::{figure} C:\Users\Tegan Goodman\Downloads\website-trial\images\Route Assignment Finder App Analysis & Design Document.pdf
:alt: Analysis and Design Document
:align: center 

Analysis and Design Document - Route Assignment Finder Application


