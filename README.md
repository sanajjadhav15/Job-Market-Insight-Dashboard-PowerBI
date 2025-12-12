# 📊 Job Market Insights Dashboard

[![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)](https://dax.guide/)

> **A comprehensive Power BI analytics project analyzing 229,000+ job postings to uncover insights about the Data Analytics job market.**

Created by **Sanaj Jadhav** 

---

## 🎯 Project Overview

This project was inspired by my personal journey navigating the Data Analytics job market. I wanted to leverage the same analytical tools I use professionally to understand:

- 🔍 Which roles are in highest demand?
- 💡 Which skills matter most to employers?
- 📍 Where are companies hiring the most?
- 💰 What are the salary trends across companies?
- 🌎 How does hiring differ by location and skill category?

The result is an **interactive 3-page Power BI dashboard** showcasing end-to-end data analytics capabilities including data cleaning, modeling, DAX calculations, and insight storytelling.

---

## 📸 Dashboard Preview

### Overview Dashboard
*Key metrics: 229K jobs analyzed, $57.33K average salary, top hiring cities and role distribution*

### Skills Demand Dashboard
*Top 10 in-demand skills and category-wise demand analysis across major cities*

### Company Hiring Insights
*Top hiring companies, market share, and salary benchmarks*

---

## 📊 Key Insights

### 💼 Job Market Trends
- **Data Analysts** (49K postings) and **Business Analysts** (39K postings) dominate the market
- **Onsite roles** remain most common (117K), followed by Hybrid (77K) and Remote (35K)
- **Chicago, IL** leads as the top hiring city

### 🛠️ Skills in Demand
Top skills across 229K job postings:
1. Business Analysis
2. Communication
3. Data Analysis
4. Data Visualization
5. Excel
6. Power BI
7. Tableau
8. SQL
9. Python
10. Statistics

### 🏢 Company Insights
- **17K companies** actively hiring
- **ClearanceJobs** leads with 4.6K postings (28.07% market share)
- **PwC** follows with 3.8K postings (22.88% market share)
- High-paying employers include: Algo Capital Group, Anthropic, DoorDash, PCS Retirement

---

## 🗂️ Data Sources

This project combines two Kaggle datasets:

### 1. **postings_cleaned**
Scraped job postings containing:
- Company details
- Location (city, country)
- Job type (Onsite/Hybrid/Remote)
- Job family and skills
- Salary information
- Posting dates

### 2. **gsearch_jobs_cleaned**
Google job search results with:
- Company names
- Location data
- Job families
- Salary ranges
- Description tokens

**Total Records:** 229,000+ job postings

---

## 🛠️ Technical Implementation

### Data Cleaning & Transformation (Power Query)
- ✅ Standardized company names across datasets
- ✅ Extracted and formatted date fields (Month, Year, Month-Year)
- ✅ Created sorting fields for chronological analysis
- ✅ Normalized location data (City, CityCountry, Country)
- ✅ Categorized skills into: Analytics Tools, Cloud, Programming, Soft Skills, Other

### Data Modeling (Star Schema)
**Fact Tables:**
- `Fact Postings` (postings_cleaned)
- `Fact Job Search` (gsearch_jobs_cleaned)
- `Fact PostingSkills`

**Dimension Tables:**
- `Dim Date`
- `Dim Company`
- `Dim Skill`
- `Dim Location`

**Relationships:** Established using PostID, LocationKey, and SkillName keys

### DAX Measures
Created custom measures for:
- **Core Metrics:** Total Jobs, Total Hiring Companies, Jobs by Role/Type
- **Location Analysis:** Top Hiring City, Jobs by Selected Skill
- **Company Metrics:** Average Jobs per Company, Average Salary
- **Advanced Calculations:** Jobs by Skill using TREATAS function

### Visualization Design
- 📍 **Page 1:** Overview with KPIs, role distribution, job types, and geographic map
- 🎯 **Page 2:** Skills analysis with top skills chart, category treemap, and city-level heatmap
- 🏢 **Page 3:** Company insights with hiring volume, market share, and salary benchmarks

---

## 💻 Technologies Used

| Technology | Purpose |
|------------|---------|
| **Power BI Desktop** | Dashboard creation and visualization |
| **Power Query** | Data cleaning and transformation |
| **DAX** | Custom calculations and measures |
| **Star Schema** | Data modeling architecture |
| **Excel/CSV** | Data source format |

---

## 🚀 Getting Started

### Prerequisites
- Power BI Desktop (latest version)
- Basic understanding of Power BI and DAX

### Installation Steps

1. **Clone the repository**
```bash
   git clone https://github.com/sanajjadhav15/Job-Market-Insight-Dashboard-PowerBI.git
```

2. **Open the Power BI file**
   - Open `Job Market Insights Dashboard.pbix` in Power BI Desktop

3. **Explore the dashboard**
   - Interact with filters and slicers
   - Navigate between the three dashboard pages
   - Examine the data model and DAX measures

### Optional: Load Custom Data
If you want to use your own datasets:
1. Place your CSV files in the `Data` folder
2. Open the Power BI file
3. Go to **Transform Data** > **Data Source Settings**
4. Update the source path to your CSV files

---

## 📈 Dashboard Features

### Interactive Elements
- 🔍 City and company filters
- 📅 Date range selection
- 🎯 Skill category filtering
- 🗺️ Geographic map with drill-through capabilities

### Key Visualizations
- **Map Visual:** Geographic distribution of job postings
- **Bar Charts:** Jobs by role, type, and company
- **Treemap:** Skill category demand
- **Heatmap:** City-level skill demand matrix
- **Donut Chart:** Company hiring market share
- **KPI Cards:** Summary metrics

---

## 🎓 Skills Demonstrated

This project showcases proficiency in:

- ✅ **Data Cleaning:** Power Query transformations and standardization
- ✅ **Data Modeling:** Star schema design with fact and dimension tables
- ✅ **DAX Proficiency:** Custom measures including TREATAS, aggregations
- ✅ **Visualization Design:** Clean, professional UI with consistent theming
- ✅ **Business Intelligence:** Translating data into actionable insights
- ✅ **Analytical Thinking:** Identifying trends and patterns in large datasets
- ✅ **Storytelling:** Presenting complex data in an accessible format

---

## 📊 Sample DAX Measures
```dax
// Total Jobs
Total Jobs = DISTINCTCOUNT('Fact Postings'[PostID])

// Average Salary
Average Salary = AVERAGE('Fact Postings'[salary])

// Top Hiring City
Top Hiring City = 
CALCULATE(
    FIRSTNONBLANK('Dim Location'[City], 1),
    TOPN(1, 
        ALL('Dim Location'[City]),
        [Total Jobs],
        DESC
    )
)

// Jobs by Skill (TREATAS)
Jobs by Skill (TREATAS) = 
CALCULATE(
    [Total Jobs],
    TREATAS(VALUES('Dim Skill'[SkillName]), 'Fact PostingSkills'[SkillName])
)
```

---

## 🔮 Future Enhancements

- [ ] Add time-series analysis for job posting trends
- [ ] Implement salary prediction model
- [ ] Create drill-through pages for detailed company analysis
- [ ] Add competitive intelligence features
- [ ] Include industry-specific breakdowns
- [ ] Integrate real-time data refresh capabilities

---

## 📝 Lessons Learned

1. **Data Quality Matters:** Significant cleaning was required to standardize company names and locations across datasets
2. **Star Schema Benefits:** Proper modeling enabled efficient filtering and cross-page interactions
3. **TREATAS Function:** Invaluable for skill analysis across multiple fact tables
4. **Visual Hierarchy:** Strategic use of KPIs and minimal formatting improved readability
5. **Business Context:** Understanding the job market personally helped identify relevant insights

---

## 👤 About Me

**Sanaj Jadhav**  
Aspiring Data Analyst | Power BI Enthusiast | Data Storyteller

I'm passionate about transforming raw data into meaningful insights that drive business decisions. This project represents my journey of applying professional analytics tools to understand the very market I'm entering.

### Connect With Me
- 💼 [LinkedIn](https://www.linkedin.com/in/sanaj-jadhav/)
- 🌐 [Portfolio](https://www.sanajjadhav.dev/)
- 📧 [Email](mailto:sanajjadhav77@gmail.com)

---

## 🙏 Acknowledgments

- **Data Sources:** Kaggle datasets on job postings
- **Tools:** Microsoft Power BI, Power Query
- **Inspiration:** Personal job search journey and desire to understand the data analytics market
- **Community:** Power BI and data analytics community for best practices

---

<div align="center">

**Made with ❤️ and Power BI**

⭐ If you found this project useful, please give it a star!

</div>
