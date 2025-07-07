README
🚗 Dynamic Parking Pricing Models
A comprehensive implementation of two dynamic parking pricing models using urban parking data to optimize parking fees based on real-time demand, traffic conditions, and various contextual factors.

## 📚 Table of Contents

1. [🔍 Overview](#overview)
2. [🤖 Models](#models)
   - [Model 1: Rule-Based Incremental Pricing](#model-1-rule-based-incremental-pricing)
   - [Model 2: Feature-Based Dynamic Pricing](#model-2-feature-based-dynamic-pricing)
3. [🗂️ Dataset](#dataset)
4. [📈 Model Performance](#model-performance)
   - [💰 Price Range](#price-range)
   - [🧠 Interpretability](#interpretability)
5. [🛠️ Technical Implementation](#technical-implementation)
6. [📌 Key Algorithms](#key-algorithms)
7. [📊 Results](#results)
8. [💡 Key Insights](#key-insights)


🔍 Overview
This project compares two dynamic pricing models used to adjust transportation fares based on real-time contextual features. The goal is to analyze how effectively each model reflects demand and environmental changes, focusing on performance, interpretability, and implementation complexity.

🤖 Models
Model 1: Rule-Based Incremental Pricing
A simple logic-based model that adjusts price based on the occupancy-to-capacity ratio:

Starts with a base price of $10.00.

Increases price incrementally using:

ini
Copy
Edit
current_price = previous_price + 0.1 * (occupancy / capacity)
Resets when the vehicle's location (Latitude/Longitude) changes.

Interpretable and lightweight, suitable for low-latency systems.

Model 2: Feature-Based Dynamic Pricing
A more advanced model that uses multiple contextual features:

Computes a raw demand score based on:

Occupancy ratio

Queue length (log-transformed)

Traffic condition (encoded numerically)

Special event days

Vehicle type (mapped to weights)

Scales the score with MinMaxScaler

Final price is calculated as:
price = BasePrice * (0.6 + λ * normalized_demand)
Prices are clipped between $5.00 and $20.00 for stability.

🗂️ Dataset
File: dataset.csv

Contains features:

Occupancy, Capacity

Latitude, Longitude

QueueLength, TrafficConditionNearby

IsSpecialDay, VehicleType

Vehicle types are mapped to weights (e.g., car=1.0, bus=2.0)

📈 Model Performance
💰 Price Range
Model 1: Price increases gradually with occupancy. Lower bound is $10.00, upper bound varies by scenario.

Model 2: Price range is clipped and consistently falls between $5.00 to $20.00.

🧠 Interpretability
Model 1 is transparent and easy to explain—ideal for rule-based deployment.

Model 2 leverages multiple interacting features—harder to interpret but offers nuanced control.

🛠️ Technical Implementation
Language: Python

Platform: Jupyter Notebook (Google Colab)

Libraries Used:

pandas, numpy

matplotlib, seaborn

sklearn.preprocessing.MinMaxScaler

Data is uploaded interactively using files.upload() in Colab

📌 Key Algorithms
Model 1: Incremental pricing algorithm based on a fixed coefficient and prior value.

Model 2:

Feature weighting and transformation (e.g., tanh, log)

Demand score calculation

Min-Max normalization

Price clipping for control

📊 Results
Histograms generated for both models showing price distributions.

Model 2 provides smoother, more bell-shaped distributions due to normalization.

Model 1 has a more jagged histogram due to stepwise increments.

💡 Key Insights
Simpler models (Model 1) are faster, more interpretable, and good for explainability.

Feature-rich models (Model 2) offer greater pricing flexibility and can better respond to complex real-time inputs.

There’s a trade-off between model complexity and deployment simplicity—choose based on use-case priorities.
