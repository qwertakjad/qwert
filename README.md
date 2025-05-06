The program can be named as a face recognition program based on PyQt5, OpenCV, Viola-jones algorithm and GUI.It contains 17 haarcascades files and 4 .py files and 4 .ui files.

1. Environment Preparation  
1.1. Install Python 3.11 , haarcascades and related libraries, as specified in `requirements.txt`:  
python==3.11  
numpy==1.14.2  
PyQt5==5.9.2  
PySocks==1.6.8  
python-telegram-bot==10.0.1  
opencv-python==3.4.1 
17 haarcascades based on OpenCV(It is stored in folder haarcascades under the same folder. They are trained datasets and used by opencv to realize face recognition and other actions easily )
Other dependencies (such as `numpy`, `sqlite3`)  
1.2. Ensure the camera is properly connected and recognized by the system.  
1.3. Place the system program and `FaceBase.db` in the same directory; if running for the first time, you can skip `FaceBase.db`, the program will create it automatically.
1.4. Prepare a computer with well camera and sound.

2. Launching the Application  
2.1. Double-click or run python ` main.py` from the command line.  
2.2. After loading, the main window pops up, containing three tabs: Face Recognition / Add  Person / Model Training.  
2.3. On the first launch, the program will detect and initialize the database; please wait for the "Database initialized successfully" log.

3. Main Interface Navigation  
Tab order: Face Recognition, Add New Person, Model Training  
The bottom and right sides of the interface always display system logs.  
The top right corner contains the function switches and parameter settings button.

4. Add Person Module  
4.1. Click the "Add New Person" tab.  
4.2, Click the “Initialize Database“ button.
4.3. Click the "Add/Update User Info" button.  
4.4. An information collection dialog will pop up:  
Enter student ID, name, preferred name, gender, age, etc.  
Click "Confirm" to submit; or "Cancel" to return.  
Click “?” if you have any question.
4.5. Click “open camera” button.
4.6. Click “Enable Face Detection” button.
4.7. Click “Start collecting face data” button.
4.8. The camera window opens:  
Click the "Capture Current Frame" button to take pictures; after each successful capture, the frame count on the right increases by 1.  
If you click "Submit" before reaching 100 frames, a collection incomplete prompt will pop up, allowing you to choose to continue or force finish.  
After capturing no less then 100 frames, click the "Submit" button to sync data:  
1. Image preprocessing: grayscale conversion, resizing to 128×128.  
2. Image enhancement: rotation, flipping, noise addition, histogram equalization (optional).  
3. Save into `./FaceBase.db/s\<stu_id>/` folder. After success, the camera closes and a collection completion prompt pops up.  
4.9. The system log records the new person's information.

5. Model Training Module  
5.1. Switch to the "Model Training" tab.  
5.2. Click the “Initialize the database” button.
5.3. View untrained records (Face ID = –1).  
5.4. Click "Initialize Database"to update the status.  
5.5. Training data preprocessing: Check on "Histogram Equalization" and click on "Image Enhancement" button.  
5.6. Click the "Start Training" button:  
1. The program calls the Viola-Jones pre-trained classifier.  
2. Train and assign Face IDs sequentially.  
3. Do not close the program during training; logs will show the progress.  
5.7. After training, all Face IDs will be updated; click "Refresh" to view the new status.
5.8. If you train the model for the first time, it's normal for this to crash or crash. You just need to wait for a while to get back to normal.

6. Face Recognition Module  
6.1. Switch to the "Face Recognition" tab.  
6.2. Upon initialization, the program automatically connects to the database and loads the model.  
6.3. In the top right corner, you can set:  
Confidence threshold (default 0.5).  
Auto-alarm threshold (default 0.3).  
Histogram equalization switch.  
Function switches: Face Tracking / Recognition / Alarm.  
6.4. Click the "turn on the camera" button:  
Real-time detection and tracking of faces: red box + "tracking…".  
Recognized faces: blue box + display name.  
Unrecognized or out-of-range faces: trigger an alarm (sound + "alarming!!!") and automatically restart the camera process.  
6.5. The bottom right of the recognition interface displays logs and alarm records in real-time.

7. System Debugging Module  
In the "Face Recognition" or "Add New Person" interface, click the "Debug" button in the top right corner to enable debug mode.  
After adjusting parameters, detection boxes are drawn in real-time on the video stream, and similarity and detection coordinates are output in the logs.  
By observing false positives/misses, adjust thresholds and image preprocessing options to optimize detection performance.

8. CRUD Module (Create, Read, Update, Delete)  
8.1. In the "Add Person" or "Model Training" interface, use the "Student ID Query" input box for exact searches.  
8.2. Select records from the query result table and click "Modify" or "Delete."  
8.3. A confirmation dialog pops up before deletion to prevent misoperation.  
8.4. After modification, click "Sync to Database," and the execution result will be recorded in the log.

9. Auto-Alarm Module  
When a similarity score below the alarm threshold is detected or an unfamiliar face is detected:  
9.1. A Alarm Settings Dialog pops up, showing the sound status and retry options.  
9.2. Users can choose "Retry Detection" or "Ignore Alarm."  
9.3. After confirmation, the system automatically restarts the camera detection process.

10. Log Recording and Viewing  
10.1. Log types: DEBUG, INFO, WARNING, ERROR.  
10.2. Each interface displays logs scrolling in real-time at the bottom right.  
10.3. You can choose "Export Logs" from the menu bar to save the logs as `.log` or `.txt` files.  
10.4. To connect to a remote log server, fill in the server address and credentials in the configuration file.  
10.5. All log files are saved in a folder named after the application start time as “app.log.***”, making it easy to locate error information and for future upgrades and maintenance. Also, if here has a mistake, the mistake will also be recorded in the “app.txt” to help others to find the mistake easier.

11. Exiting the System  
11.1. Click the close button (×) at the top left corner of the main window.  
11.2. If data collection or training is in progress, an Exit Confirmation Dialog will pop up, allowing you to choose "Confirm Exit" or "Cancel."  
11.3. After confirmation, the program will sequentially close the camera, save logs, release resources, and exit.

12. Exception Handling  
Camera cannot open: Check USB connection, drivers, or modify the camera index in the configuration.  
Database connection failure: Check `FaceBase.db` file path and read/write permissions.  
Program crash/freeze: Since model training may take a long time, temporary crashes or freezes can occur. After waiting a while, locate the error through the logs. You can reproduce and fix it in debug mode.  
False alarm triggers: Adjust the alarm threshold or reposition the camera and adjust lighting conditions.

13.If you have any questions about my code and illustrate or any other things, feel free to contact me. My email is bson0733@uni.sydney.edu.au.
