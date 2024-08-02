from flask import Flask, request, jsonify

app = Flask(__name__)

# User details (you can set these dynamically or fetch from a database)
USER_ID = "john_doe_17091999"
EMAIL = "john@xyz.com"
ROLL_NUMBER = "ABCD123"

@app.route('/bfhl', methods=['POST'])
def bfhl_post():
    try:
        # Extracting the data from the request JSON
        data = request.json.get('data', [])
        
        # Separating numbers and alphabets
        numbers = [item for item in data if item.isdigit()]
        alphabets = [item for item in data if item.isalpha()]
        
        # Finding the highest alphabet (last in the A-Z series)
        highest_alphabet = [max(alphabets, key=lambda x: x.lower())] if alphabets else []
        
        response = {
            "is_success": True,
            "user_id": USER_ID,
            "email": EMAIL,
            "roll_number": ROLL_NUMBER,
            "numbers": numbers,
            "alphabets": alphabets,
            "highest_alphabet": highest_alphabet
        }
        return jsonify(response), 200
    
    except Exception as e:
        # Handling unexpected errors
        return jsonify({"is_success": False, "error": str(e)}), 400

@app.route('/bfhl', methods=['GET'])
def bfhl_get():
    # Returning a hardcoded operation_code for GET requests
    return jsonify({"operation_code": 1}), 200

if __name__ == '__main__':
    app.run(debug=True)
