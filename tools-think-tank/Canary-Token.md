# Canary Token in Microsoft Word for Intrusion Detection

## 1. What is a Canary Token?
A **Canary Token** is a trap file that sends an alert when accessed or opened. It is particularly useful for detecting intrusions or unauthorized actions on your system or network.  
In the context of a Microsoft Word document, a Canary Token can execute a hidden action (e.g., sending an HTTP request or email) whenever the file is opened.

---

## 2. Steps to Create a Word Document Canary Token

### Option 1: Using VBA Script
You can embed a VBA macro in a Word document to trigger an alert or log the access event.

#### Steps:
1. **Open Microsoft Word**:
   - Create a new Word document.

2. **Enable Developer Tab**:
   - Go to `File > Options > Customize Ribbon`.
   - Check the **Developer** tab to enable it.

3. **Access the VBA Editor**:
   - Click on `Developer > Visual Basic`.
   - Alternatively, press `Alt + F11`.

4. **Add the VBA Script**:
   - In the VBA editor, double-click `ThisDocument` in the left pane.
   - Add the following code:
     ```vba
     Private Sub Document_Open()
         ' Trigger a web request to your monitoring server
         Dim http As Object
         Set http = CreateObject("MSXML2.XMLHTTP")
         On Error Resume Next
         http.Open "GET", "http://your-server-ip/canary-trigger", False
         http.Send
     End Sub
     ```
     Replace `http://your-server-ip/canary-trigger` with the URL of your monitoring server.

5. **Save the Document**:
   - Save the file as a macro-enabled Word document:
     - `File > Save As > Word Macro-Enabled Document (.docm)`.

6. **Test the Document**:
   - Open the document and verify if the HTTP request is triggered.  
   - Use tools like **Wireshark** or server logs to confirm.

---

### Option 2: Using an Embedded Link
Alternatively, use a clickable link or an embedded object in the Word document as the Canary Token.

#### Steps:
1. **Insert a Hyperlink**:
   - Highlight some text in the document.
   - Press `Ctrl + K` or right-click and select **Hyperlink**.
   - Use the link `http://your-server-ip/canary-trigger`.

2. **Embed an Image with a Hyperlink**:
   - Insert an image into the document.
   - Right-click the image and select **Hyperlink**.
   - Add the URL to your monitoring server.

---

## 3. Setting Up the Monitoring Server
To make your Canary Token effective, you need a monitoring server to log or alert when the token is triggered.

### Options for Monitoring Server:
#### Simple Python HTTP Server:
Start a basic server to log requests:
```bash
python3 -m http.server 80
```
Any access to `http://your-server-ip/canary-trigger` will be logged.

#### Custom Flask Application:
Create a robust server with email or SMS alerts:
```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/canary-trigger', methods=['GET'])
def canary():
    print(f"Canary triggered by: {request.remote_addr}")
    # Add email or webhook notification here
    return "OK"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

#### CanaryTokens.org:
Use the free service from [CanaryTokens.org](https://canarytokens.org/) to generate a pre-built token URL for monitoring.

---

## 4. Use Cases for the LAN-KALI Project
### Demonstrating Data Exfiltration Detection:
- Simulate an attacker accessing sensitive files by placing a Word document that triggers an alert when opened.

### Highlighting Insider Threats:
- Place the document in a shared folder and monitor unauthorized access by users on the LAN.

### Integrating with the Kali LAN Storyline:
- Plant the token as a decoy in **Mimi Palmer’s Orchid Shop Cybersecurity Lab**.

---

## 5. Security Considerations
- **Macro Security**: Modern versions of Word disable macros by default. You may need to enable macros for testing.
- **Monitoring Server Exposure**: Ensure your monitoring server is secure to avoid exploitation.
- **Legal Compliance**: Only use Canary Tokens in environments you own or have explicit permission to test.

---

## Conclusion
Using Canary Tokens with a Microsoft Word document is an effective way to demonstrate intrusion detection within the **LAN-KALI Project**. A VBA macro or embedded link acts as the trigger, while a simple monitoring server captures the access event. This approach provides a real-world example of detecting unauthorized actions.

