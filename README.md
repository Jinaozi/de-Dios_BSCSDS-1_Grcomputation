from flask import Flask, request, render_template_string

app = Flask(__name__)

def compute_grades(prelim, midterm=None, final=None):
    prelim_weight = 0.20
    midterm_weight = 0.30
    final_weight = 0.50
    if not 0 <= prelim <= 100:
        return "Prelim grade must be between 0 and 100."
    if prelim < 75:
        passing_grade = 75.0
        needed_grade = passing_grade - (prelim_weight * prelim)
        # Calculate required grades
        required_midterm = needed_grade / midterm_weight
        required_final = needed_grade / final_weight
        # Cap required grades to a maximum of 100
        if required_midterm > 100:
            required_midterm = 100
        if required_final > 100:
            required_final = 100        
        return (f"Required Midterm Grade to Pass: {required_midterm:.2f}, "
                f"Required Final Grade to Pass: {required_final:.2f}")
    else:
        # Check for Dean's List qualification
        if prelim > 90:
            return "Congratulations! You qualify for the Dean's List."
        else:
            return "No worries, you passed bestie!"

@app.route('/', methods=['GET', 'POST'])
def index():
    result = ""
    if request.method == 'POST':
        try:
            prelim = float(request.form['prelim'])
            midterm = request.form.get('midterm', None)
            final = request.form.get('final', None)          
            if midterm:
                midterm = float(midterm)
            else:
                midterm = None
            if final:
                final = float(final)
            else:
                final = None
            result = compute_grades(prelim, midterm, final)
        except ValueError:
            result = "Please enter valid numerical values for grades."
    return render_template_string('''
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Grade Computation Tool</title>
        <style>
            body {
                font-family: Monospace;
                background-color: #B0BBD2;
                margin: 20px;
                padding: 20px;
                display: flex;
                justify-content: center;
                align-items: center;
                height: 50vh;
            }
            .container {
                max-width: 600px;
                margin: auto;
                padding: 20px;
                border: 4px solid #D1656B;
                border-radius: 13px;
                background-color: #F9B6A1;
                box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            }
            .result {
                margin-top: 20px;
                padding: 10px;
                background-color: #E6E0D0;
            }
        </style>
    </head>
    <body>
        <div class="container">
            <h1>Grade Computation Tool</h1>
            <form method="post">
                <label for="prelim">Enter your Prelim grade (required):</label>
                <input type="number" id="prelim" name="prelim" min="0" max="100" step="0.01" required><br><br>
                <label for="midterm">Enter your Midterm grade:</label>
                <input type="number" id="midterm" name="midterm" min="0" max="100" step="0.01"><br><br>
                <label for="final">Enter your Final grade:</label>
                <input type="number" id="final" name="final" min="0" max="100" step="0.01"><br><br>
                <button type="submit">Compute</button>
            </form>
            <div id="result" class="result">
                <h2>Result</h2>
                <div>{{ result }}</div>
            </div>
        </div>
    </body>
    </html>
    ''', result=result)

if __name__ == '__main__':
    app.run(debug=True)
