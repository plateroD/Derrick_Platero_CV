# Derrick_Platero_CV
I am trying to create my CV on here and edit it because I have new things to add. 

template = """
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ name }}&#39;s CV</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; line-height: 1.6; }
        h1, h2 { color: #003366; }
        .section { margin-bottom: 20px; }
        .section h2 { border-bottom: 1px solid #003366; padding-bottom: 5px; }
        .subheading { font-weight: bold; }
        .details { font-style: italic; }
    </style>
</head>
<body>
    <h1>{{ name }}</h1>
    <p><strong>Phone:</strong> {{ phone }}<br>
       <strong>Email:</strong> {{ email }}<br>
       <strong>GitHub:</strong> <a href="{{ github }}">{{ github }}</a><br>
       <strong>LinkedIn:</strong> <a href="{{ linkedin }}">{{ linkedin }}</a></p>

    <div class="section">
        <h2>Education</h2>
        {% for edu in education %}
        <h3>{{ edu.degree }} in {{ edu.field }} - {{ edu.university }}</h3>
        <p class="details">{{ edu.details }}</p>
        {% endfor %}
    </div>

    <div class="section">
        <h2>Research Experience</h2>
        {% for exp in experience %}
        <h3>{{ exp.title }} - {{ exp.institution }}</h3>
        <p class="details">{{ exp.dates }}</p>
        <ul>
            {% for item in exp.details %}
            <li>{{ item }}</li>
            {% endfor %}
        </ul>
        {% endfor %}
    </div>

    <div class="section">
        <h2>Skills</h2>
        <ul>
            {% for skill in skills %}
            <li>{{ skill }}</li>
            {% endfor %}
        </ul>
    </div>

    <div class="section">
        <h2>Publications</h2>
        <ul>
            {% for pub in publications %}
            <li>{{ pub }}</li>
            {% endfor %}
        </ul>
    </div>
</body>
</html>
"""
################This is the "meat and potatoes" of the CV that lists my accomplsihments, education, awards, etc. 

data = {
    "name": "Derrick Platero",
    "phone": "(505) 785-9404",
    "email": "dplatero@iastate.edu",
    "github": "https://github.com/plateroD",
    "linkedin": "https://linkedin.com/in/derrick-platero",
    "education": [
        {
            "degree": "PhD in Soil Science",
            "field": "Soil Science and Geomorphology",
            "university": "Iowa State University",
            "location": "Ames, IA",
            "expected_completion": "05/2028",
            "dissertation": "Validating Hillslope Erosion Models: From Soil Science to Geomorphology",
            "advisor": "Bradley Miller",
            "gpa": "3.7/4.0",
            "highlights": "Research focus: Comparing geomorphological and agricultural models of sediment transport and elevation changes, validating the results against real-world data."
        },
        {
            "degree": "Master of Science in Soil Science",
            "field": "Soil Science",
            "university": "University of Georgia",
            "location": "Athens, GA",
            "expected_completion": "05/2022",
            "thesis": "Determining Optimal Sample Size for Soil Texture Mapping in a Georgia Piedmont Floodplain, USA",
            "advisor": "Matthew Levi & Nandita Gaur",
            "gpa": "3.42/4.0",
            "highlights": ""
        }
    ],
    "experience": [
        {
            "position": "Graduate Research Assistant",
            "institution": "Iowa State University",
            "location": "Ames, IA",
            "dates": "01/2023 - Present",
            "details": [
                "Researching and comparing geomorphological and agricultural models of sediment transport and elevation changes.",
                "Validating model results against observed data.",
                "Conducting statistical analysis and machine learning validation techniques."
            ]
        }
    ],
    "skills": ["Programming: R, C++, Python (NumPy, Pandas, Matplotlib)", "GIS: ArcGIS, LiDAR analysis"],
    "publications": [
        "Platero, D., Levi, M., Gaur, N. (2023). Determining optimal sample size for soil texture mapping in a Georgia Piedmont floodplain, USA. Soil Science Society of America Journal. (pending)."
    ]
}

############################# Jinja2's Environment and FileSystemLoader to load an external HTML template file (cv_template.html) and populate it with the data you provide in a Python dictionary (data).F ########################

from jinja2 import Environment, FileSystemLoader
import pdfkit

# Correct the path to point to the directory containing the template
file_loader = FileSystemLoader(r'F:\GitHub resp\CV')

# Initialize the environment with the loader
env = Environment(loader=file_loader)

# Now, use only the filename in get_template
template = env.get_template('cv_template.html')

# Define your data dictionary here (make sure it's defined before this step)
data = {
    # Your data structured as a dictionary
}

# Render the template with your data
output = template.render(data)

# Save the rendered HTML to a file (optional, for debugging)
with open('output.html', 'w') as f:
    f.write(output)

# Specify the path to wkhtmltopdf
path_wkhtmltopdf = r'C:\Program Files\wkhtmltopdf\bin\wkhtmltopdf.exe'
config = pdfkit.configuration(wkhtmltopdf=path_wkhtmltopdf)

# Convert HTML to PDF
pdfkit.from_string(output, 'output.pdf', configuration=config)


######################### Once the template is populated with data, it is rendered as HTML, and then you are using pdfkit (which internally uses wkhtmltopdf) to convert the HTML into a PDF #########

# Specify the path to wkhtmltopdf
path_wkhtmltopdf = r'C:\Program Files\wkhtmltopdf\bin\wkhtmltopdf.exe'
config = pdfkit.configuration(wkhtmltopdf=path_wkhtmltopdf)

# Convert HTML to PDF
pdfkit.from_string(output, 'output.pdf', configuration=config)
