# Fridge Friend - Smart Inventory System

## Team Information

**ENSC Capstone 1244 - Company 09**  
**Project Duration:** May 2024 to December 2024

## Project Overview

In today's fast-paced world, food waste and dietary concerns are becoming issues of increasing concern. With many people spending upwards of eight hours per day at work or school, families often struggle to keep their refrigerators organized. Without a system to track the groceries in the fridge, ingredients are often forgotten and ultimately wasted. Additionally, simple, nutritious and tailored recipes can be hard to come by without specific knowledge of the ingredients within the fridge.

**Fridge Friend** offers a unique and innovative solution to these challenges by addressing both nutritional concerns and food waste. Utilizing a fine-tuned machine learning model, Fridge Friend tracks all items entering and leaving the fridge and suggests recipes based on available ingredients. It detects when food items are being placed into or taken out of the fridge, then identifies them in real-time. This data is then sent to a cloud server, allowing users to access a complete list of their ingredients through an integrated user interface. With nutrition and simplicity at the forefront, tailored recipes can be suggested based on the user's available ingredients.

## System Architecture

### Edge-to-Cloud Design

**Local Processing (Raspberry Pi):**
- Real-time computer vision processing using YOLOv10
- Barcode detection via OpenCV/ZBar
- Local inference to maximize privacy
- Sensor monitoring for fridge door events

**Cloud Infrastructure (AWS EC2):**
- Central inventory database
- REST API server for data synchronization
- Recipe suggestion engine
  
**Data Flow:**
1. Raspberry Pi detects food items via camera when fridge door opens
2. Local processing identifies items using YOLOv10 or barcode scanning
3. Detection results sent to AWS EC2 server via REST API
4. Server updates inventory database in real-time
5. Users access current inventory through web interface
6. Recipe suggestions generated based on available ingredients


## Hardware Design

### CAD Model
<p align="center">
  <img width="700" alt="Fridge Friend CAD Model" src="https://github.com/user-attachments/assets/71b03507-1cad-4dc9-b488-ffb717b5db79" />
  <br>
  <em>3D CAD model showing the camera housing and sensor mounting system</em>
</p>

### Final Assembly
<p align="center">
  <img src="https://github.com/user-attachments/assets/244a71a3-a55c-4961-b040-5fbb706548ae" alt="Fridge Friend Final Assembly" width="700"/>
  <br>
  <em>Completed hardware assembly installed in refrigerator with Raspberry Pi, camera module, and sensors</em>
</p>

The hardware design features:
- Custom 3D-printed camera housing for refrigerator mounting
- Integrated Raspberry Pi compartment with thermal management
- Optimized camera angle for full shelf coverage
- Weatherproof enclosure for refrigerator environment
- Easy installation with magnetic mounting system

## Repository Structure

```
.
├── Backend/
│   ├── importRecipes.mjs   # Builds the SQLite recipe database from recipe.csv
│   ├── recipe.csv          # Source recipe data
│   ├── recipes.db          # Generated SQLite recipe database
│   ├── api.py              # Small Python client for posting test ingredient updates
│   └── package.json
├── UI/
│   ├── server.js           # Express + Socket.IO web server (port 3000)
│   ├── recipes.db          # SQLite recipe database served by the app
│   ├── public/             # Front end: index.html, script.js, styles.css, images, Ingredients.csv
│   └── package.json
└── README.md
```

The on-device computer vision and detection code runs on the Raspberry Pi and is deployed separately from this repository, which contains the web application and recipe backend.

## Getting Started

### Prerequisites
- Node.js and npm
- (Optional) Python 3 with the `requests` package, for the sample API test client

### Run the web app
```bash
cd UI
npm install
node server.js
```
Then open http://localhost:3000 in your browser. The server serves the interface, exposes REST endpoints for managing inventory and fetching recipes, and opens a Socket.IO channel for real-time "session complete" notifications.

### Recipe database
A prebuilt `recipes.db` is included with the app. To regenerate it from `recipe.csv`:
```bash
cd Backend
npm install
node importRecipes.mjs
```

### Inventory data
Current fridge contents are stored in `UI/public/Ingredients.csv` as `name,date` rows. The server reads and updates this file as items are added, edited, or removed through the interface, and recipe suggestions are matched against these ingredients.

## Key Features

- **Real-Time Food Detection:** Computer vision-powered system that automatically identifies produce and packaged goods
- **Inventory Tracking:** Maintains an up-to-date record of all items in your refrigerator
- **Barcode Recognition:** Dual detection system supporting both visual recognition and barcode scanning
- **Recipe Suggestions:** Intelligent recipe recommendations based on available ingredients
- **Cloud Synchronization:** Access your inventory from anywhere through our user interface
- **Food Waste Reduction:** Track expiration dates and receive notifications to minimize waste
- **Nutritional Insights:** Make informed dietary choices with ingredient-aware recipe suggestions

## Technical Achievements

### Computer Vision & Machine Learning
- Fine-tuned **YOLOv10** model trained on 5,000+ images using Ultralytics
- Achieved **94% F1-score** across 12 produce categories
- Real-time object detection for instant ingredient identification

### Backend Infrastructure
- Built a **Node.js and Express** REST API with **Socket.IO** for real-time inventory updates
- Real-time inventory updates from multiple input sources (computer vision + barcode scanning)
- Robust error handling and data validation

### Product Identification System
- Integrated **OpenFoodFacts API** with over 3 million database entries
- **OpenCV/ZBar** barcode detection pipeline
- **95% accuracy** in product identification
- Hybrid detection system combining visual and barcode recognition

## Technologies Used

### Machine Learning & Computer Vision
- YOLOv10 (Ultralytics)
- OpenCV
- Python
- PyTorch

### Backend & API
- Node.js and Express
- Socket.IO (real-time notifications)
- SQLite (recipe database)
- CSV-based ingredient inventory
- OpenFoodFacts API (barcode lookups)
- ZBar (barcode processing)

### Hardware
- Raspberry Pi (local processing and detection)
- Camera module for real-time detection
- Sensor integration for fridge door monitoring

### Cloud & Deployment
- AWS EC2 (server hosting and API deployment)
- Cloud database for inventory synchronization
- REST API endpoints for Pi-to-server communication

### Architecture Benefits
- **Edge Processing:** YOLOv10 inference runs locally on Pi, maximizing privacy
- **Cloud Storage:** Centralized inventory accessible from any device
- **Scalability:** Multiple Raspberry Pi units could connect to a single EC2 server (with future development)
- **Reliability:** Local processing continues even if network connection is temporarily lost

## Impact & Benefits

### Food Waste Reduction
- Automatic tracking prevents forgotten ingredients
- Expiration date monitoring reduces spoilage

### Nutritional Benefits
- Ingredient-aware recipe suggestions
- Dietary preference customization
- Promotes home cooking with available ingredients

### Convenience
- Hands-free inventory management
- Remote access to fridge contents
- Automated shopping list generation

## Future Enhancements

- [ ] Expand to 50+ produce categories
- [ ] Integration with smart home ecosystems
- [ ] Mobile app development (iOS/Android)
- [ ] Meal planning and scheduling features
- [ ] Multi-user household support
- [ ] Carbon footprint tracking
- [ ] Integration with grocery delivery services

*Fridge Friend - Reducing food waste, one ingredient at a time.*
