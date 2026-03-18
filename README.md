# Instructor-Performance-Analysis

### Table of Contents
- [Project Overview](#project-overview)
- [The Challenge](#the-challenge)
- [Data Architecture](#data-architecture)
- [Defining Effectiveness](#defining-effectiveness)
- [Techincal Workflow](#technical-workflow)
- [Key Insights](#key-insights)
- [Model Performance](#model-performance)
- [EdTech Product Recommendations](#edtech-product-recommendations)
- [Setup and How to Run](#setup-and-how-to-run)

### Project Overview
This project focuses on identifying the drivers of successful teaching in an online learning environment. By analyzing batch level metrics across different instructors and courses, we built a multi-dimensional "Effectiveness Score" and a Machine Learning model to predict instructor performance tiers based purely on student engagement behaviors.

### The Challenge
In EdTech, judging an instructor solely on a 5-star rating is misleading. A "charismatic" teacher might have high ratings but low student completion. Conversely, a "tough" teacher might have low ratings but high quiz scores. This project creates a balanced scorecard to solve this problem.

### Data Architecture
The analysis processes a dataset of 2,000+ course batches utilizing:
1. Outcome Metrics: Completion rates, dropout rates and average quiz scores.
2. Engagement Metrics: Video watch time, forum activity and assignment submission rates.
3. Feedback Metrics: Qualitative learner ratings (1–5) and feedback response rates.

### Defining Effectiveness
We defined a custom Instructor Effectiveness Score using a weighted formula to ensure a holistic view of performance:
- 40% Completion Rate: The primary KPI did the student reach the finish line?
- 30% Academic Rigor: Measured by average quiz scores and score improvement.
- 30% Learner Satisfaction: Normalized feedback scores to capture the student experience.
Instructors are then categorized into Low, Medium and High tiers based on these scores.

### Technical Workflow
1. Data Sanitization: Handled missing values using median imputation for scores and zero filling for engagement activity.
2. Aggregation Logic: Batches were rolled up to the instructor_id level. We introduced a Confidence Level feature to distinguish between veteran instructors and new instructors.
3. Predictive Modeling: Trained a Random Forest Classifier to predict an instructor's tier.

### Key Insights
- Assignment submission rates were the strongest predictor of a "High" effectiveness tier, outweighing simple video watch time.
- Aggregation revealed that "High" tier instructors maintain low variance in dropout rates across multiple different courses.

### Model Performance
The Random Forest model was evaluated on its ability to correctly classify the performance tier of a batch based on early stage engagement data.
| Metric | Low Tier | Medium Tier | High Tier |
| :--- | :---: | :---: | :---: |
| **Precision** | 0.82 | 0.78 | 0.85 |
| **Recall** | 0.80 | 0.75 | 0.88 |
| **F1-Score** | 0.81 | 0.76 | 0.86 |

### EdTech Product Recommendations
1. If a batch's "Assignment Submission Rate" drops below 0.5 within the first week, flag the instructor for a "Student Nudge" intervention.
2. Use the weighted Effectiveness Score to highlight top performing instructors for marketing and promotion.

### Setup and How to Run
1. Installation
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```
2. Execution
The analysis is contained within a single Jupyter Notebook. Ensure the dataset URL is accessible and run all cells:
```bash
jupyter notebook Instructor_Effectiveness_Analysis.ipynb
```
