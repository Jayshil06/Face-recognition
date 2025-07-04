🎯 Face Recognition Attendance System
A real-time attendance system using Face Recognition technology with OpenCV, face_recognition, and Firebase as a backend for storing student data and attendance records.

📸 Recognize faces live via webcam, 📊 track attendance automatically, and 🔥 sync data to Firebase in real-time.

🚀 Features
✅ Real-time Face Recognition
Identify students instantly using your webcam.

✅ Firebase Integration
Store student profiles and attendance records in Firebase Realtime Database & Cloud Storage.

✅ Attendance Tracking
Mark attendance with total counts & timestamps automatically.

✅ User Interface
Displays student details and attendance status on a custom background image.

✅ Data Management
Utility script to add initial student data to Firebase effortlessly.

🛠️ Technologies Used
Technology	Purpose
🐍 Python	Core programming language
📷 OpenCV (cv2)	Real-time video capture & UI rendering
🧠 face_recognition	Face detection & recognition
🔥 Firebase Admin SDK	Backend database & storage integration
📦 numpy	Numerical operations with image data
💻 cvzone	Simplifies OpenCV tasks
📅 datetime	Attendance timestamping
📊 openpyxl, xlwt	(Optional) Excel file operations

📁 Project Structure
bash
Copy
Edit
Face-recognition/
├── main.py                  # Real-time recognition & attendance
├── addingDatatoDatabase.py  # Adds initial student data to Firebase
├── EncodeGenerator.py       # Generates face encodings (to create)
├── Resources/
│   ├── background.png
│   └── Modes/               # UI mode images
├── Images/                  # Student face images
├── Encodings.p              # Pickle file with face encodings
├── serviceAccountKey.json   # Firebase service account key (secure!)
├── README.md
└── requirements.txt
⚡ Quick Start
1️⃣ Clone the Repository
bash
Copy
Edit
git clone https://github.com/Jayshil06/Face-recognition.git
cd Face-recognition
2️⃣ Install Dependencies
It’s recommended to use a virtual environment.

bash
Copy
Edit
pip install -r requirements.txt
If requirements.txt isn’t available:

bash
Copy
Edit
pip install opencv-python face_recognition firebase-admin numpy cvzone openpyxl xlwt xlutils
3️⃣ Firebase Setup
Create Firebase Project: Firebase Console → Add new project

Enable Realtime Database & Cloud Storage

Generate Service Account Key:

Go to ⚙️ Project settings → Service accounts

Click Generate new private key

Download serviceAccountKey.json

Place it in your project root folder (DO NOT share this file)

4️⃣ Add Student Data
Edit addingDatatoDatabase.py with your students:

python
Copy
Edit
data = {
    "1001": {
        "name": "John Doe",
        "major": "Computer Science",
        "starting_year": 2022,
        "total_attendance": 0,
        "standing": "G",
        "year": 3,
        "last_attendance": "2024-07-01 09:00:00"
    },
    ...
}
Run the script:

bash
Copy
Edit
python addingDatatoDatabase.py
5️⃣ Generate Face Encodings
Create EncodeGenerator.py:

python
Copy
Edit
import cv2, face_recognition, pickle, os

folderPath = 'Images'
pathList = os.listdir(folderPath)
imgList, studentIds = [], []

for path in pathList:
    imgList.append(cv2.imread(os.path.join(folderPath, path)))
    studentIds.append(os.path.splitext(path)[0])  # Image names as IDs

print("Encoding Started ...")
encodeListKnown = []
for img in imgList:
    imgRGB = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    encodes = face_recognition.face_encodings(imgRGB)
    if encodes:
        encodeListKnown.append(encodes[0])

file = open("Encodings.p", 'wb')
pickle.dump([encodeListKnown, studentIds], file)
file.close()
print("Encoding Complete & File Saved")
Run:

bash
Copy
Edit
python EncodeGenerator.py
6️⃣ Start the Application
Make sure your webcam is connected:

bash
Copy
Edit
python main.py
🖥️ How It Works
📌 Point your webcam at a student’s face:

✅ If recognized → displays student info & marks attendance.

🗓 Updates total attendance & last timestamp in Firebase.

📊 Shows: Name, Major, Year, Standing, Total Attendance.

📸 Demo (Screenshots)
Webcam Detection	Firebase Attendance Record

🤝 Contributing
Pull requests are welcome! 🚀

Fork the repo

Create a branch:

bash
Copy
Edit
git checkout -b feature/your-feature
Commit your changes:

bash
Copy
Edit
git commit -m 'Add some feature'
Push to the branch:

bash
Copy
Edit
git push origin feature/your-feature
Open a Pull Request


