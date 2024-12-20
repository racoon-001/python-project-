# python-project-
import pandas as pd

# Sample data for job applications
data = {
    "Name": ["Alice", "Bob", "Charlie", "Diana", "Eve"],
    "Experience (years)": [5, 2, 7, 3, 1],
    "Skills": [
        "Python, Machine Learning, SQL",
        "Java, Spring Boot, MySQL",
        "Python, Data Analysis, SQL",
        "HTML, CSS, JavaScript",
        "Python, Flask, Django"
    ],
    "Education": [
        "Bachelor's",
        "Master's",
        "Bachelor's",
        "Bachelor's",
        "Master's"
    ]
}

# Create a DataFrame
applications = pd.DataFrame(data)

# Define shortlisting criteria
MIN_EXPERIENCE = 3
REQUIRED_SKILLS = {"Python", "SQL"}
REQUIRED_EDUCATION = "Bachelor's"

# Shortlisting function
def shortlist_applicants(df):
    shortlisted = []

    for index, row in df.iterrows():
        # Check experience
        if row["Experience (years)"] < MIN_EXPERIENCE:
            continue

        # Check skills
        applicant_skills = set(row["Skills"].split(", "))
        if not REQUIRED_SKILLS.issubset(applicant_skills):
            continue

        # Check education
        if row["Education"] != REQUIRED_EDUCATION:
            continue

        # If all criteria are met, add to shortlisted
        shortlisted.append(row["Name"])

    return shortlisted

# Shortlist applicants
shortlisted_candidates = shortlist_applicants(applications)

# Display shortlisted candidates
print("Shortlisted Candidates:")
for candidate in shortlisted_candidates:
    print(candidate)
