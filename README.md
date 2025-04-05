from flask import Flask
import os
import time
import subprocess

app = Flask(__name__)

@app.route('/htop')
def htop():
    name = "Your Full Name"
    username = os.getenv("USER")
    server_time = time.strftime("%Y-%m-%d %H:%M:%S", time.localtime())
    top_output = subprocess.check_output(['top', '-b', '-n', '1']).decode('utf-8')
    return f"""
    <html>
        <body>
            <h1>HTop Endpoint</h1>
            <p><strong>Name:</strong> {name}</p>
            <p><strong>Username:</strong> {username}</p>
            <p><strong>Server Time (IST):</strong> {server_time}</p>
            <pre>{top_output}</pre>
        </body>
    </html>
    """

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8080)
