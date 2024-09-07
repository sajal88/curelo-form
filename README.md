<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MER Details Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #f4f4f4;
        }
        .form-container {
            background: #fff;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0,0,0,0.1);
            max-width: 800px;
            width: 100%;
            box-sizing: border-box;
        }
        h1 {
            text-align: center;
            margin-bottom: 20px;
            color: #333;
        }
        .form-group {
            margin-bottom: 20px;
        }
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #333;
        }
        .form-group input[type="text"],
        .form-group input[type="number"],
        .form-group input[type="date"],
        .form-group input[type="file"] {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 5px;
            box-sizing: border-box;
        }
        .form-group input[readonly] {
            background-color: #e9ecef;
            cursor: not-allowed;
        }
        .form-group input[type="radio"] {
            margin-right: 10px;
        }
        .form-group .gender-label {
            display: inline-block;
            margin-right: 15px;
        }
        .form-group button {
            width: 100%;
            padding: 12px;
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
        }
        .form-group button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="form-container">
        <h1>MER Details Form</h1>
        <form name = 'submit-to-google-sheet' id="merForm" enctype="multipart/form-data">

          <div class="form-group">
                <label>Phone Number:</label>
                <input type="text" id="phone" name="PhoneNo" placeholder="XXXXXXXXXX" pattern="[6789]\d{9}" title="Please enter a valid 10-digit phone number." >
            </div>
          
            <div class="form-group">
                <label for="customerId">Customer ID:</label>
                <input type="text" id="customerId" name="CustomerId" >
            </div>

            <div class="form-group">
                <label for="customerName">Customer Name:</label>
                <input type="text" id="customerName" name="CustomerName" pattern="[A-Za-z\s]+" title="Name must contain only alphabets." >
            </div>

            <div class="form-group">
                <label for="customerAddress">Customer Address:</label>
                <input type="text" id="customerAddress" name="CustomerAddress" >
            </div>

            <div class="form-group">
                <label for="pincode">Pincode:</label>
                <input type="text" id="pincode" name="Pincode" pattern="\d{6}" title="Please enter a valid 6-digit pincode." >
            </div>

            <div class="form-group">
                <label for="dob">Date of Birth:</label>
                <input type="date" id="dob" name="DOB" >
            </div>

            <div class="form-group">
                <label>Gender:</label>
                <label class="gender-label">
                    <input type="radio" id="male" name="Gender" value="Male" > Male
                </label>
                <label class="gender-label">
                    <input type="radio" id="female" name="Gender" value="Female"> Female
                </label>
                <label class="gender-label">
                    <input type="radio" id="other" name="Gender" value="Other"> Other
                </label>
            </div>

            <div class="form-group">
                <label for="weight">Weight (kg):</label>
                <input type="number" id="weight" name="Weight" step="1" min="0" max="200" >
            </div>

            <div class="form-group">
                <label for="weightImage">Upload Weight Image:</label>
                <input type="file" id="weightImage" name="WeightImage" accept="image/*" capture="camera" >
            </div>

            <div class="form-group">
                <label for="height">Height (cm):</label>
                <input type="number" id="height" name="Height" step="1" min="0" max="999" >
            </div>

            <div class="form-group">
                <label for="heightImage">Upload Height Image:</label>
                <input type="file" id="heightImage" name="HeightImage" accept="image/*" capture="camera" >
            </div>

            <div class="form-group">
                <label for="bp1">First Blood Pressure Reading:</label>
                <input type="text" id="bp1" name="BP1" placeholder="Systolic/Diastolic" pattern="\d{2,3}/\d{2,3}" title="Please enter a valid blood pressure reading in Systolic/Diastolic format." >
            </div>

            <div class="form-group">
                <label for="bp2">Second Blood Pressure Reading:</label>
                <input type="text" id="bp2" name="BP2" placeholder="Systolic/Diastolic" pattern="\d{2,3}/\d{2,3}" title="Please enter a valid blood pressure reading in Systolic/Diastolic format." >
            </div>

            <div class="form-group">
                <label for="bp3">Third Blood Pressure Reading:</label>
                <input type="text" id="bp3" name="BP3" placeholder="Systolic/Diastolic" pattern="\d{2,3}/\d{2,3}" title="Please enter a valid blood pressure reading in Systolic/Diastolic format." >
            </div>

            <div class="form-group">
                <label for="halfPhoto">Upload Half Photo:</label>
                <input type="file" id="halfPhoto" name="HalfPhoto" accept="image/*" capture="camera" onchange= "HandleFileChange(event, 'halfPhoto')" >
            </div>

            <div class="form-group">
                <label for="fullPhoto">Upload Full Photo:</label>
                <input type="file" id="fullPhoto" name="FullPhoto" accept="image/*" capture="camera" onchange = "HandleFileChange(event, 'fullPhoto')">
            </div>
            <input type="hidden" id="latitude" name="Latitude">
            <input type="hidden" id="longitude" name="Longitude">

            <div class="form-group">
                <button type="submit">Submit</button>
            </div>
            <br>
          <span id="success"> </span>
        </form>
    </div>

    <script>
      const scriptURL = 'https://script.google.com/macros/s/AKfycbz2fwS2UQYrjM27U0a3630M-y08PVsFDwvplnOZ4LMLJAURTvSJjlacM7cx3JykdTJT/exec'
      const form = document.forms['submit-to-google-sheet'];
        const success = document.getElementById('success');

        form.addEventListener('submit', e => {
            e.preventDefault();
            fetch(scriptURL, { method: 'POST', body: new FormData(form) })
                .then(response => {
                    success.innerHTML = "Data Successfully Submitted";
                    setTimeout(function() {
                        success.innerHTML = "";
                    }, 5000);
                    form.reset();
                })
                .catch(error => {
                    console.error('Error!', error.message);
                    success.innerHTML = "Failed to submit data.";
                });
        });
       function HandleFileChange(event, imageType) {
            const file = event.target.files[0];
            if (file && file.type.startsWith('image/')) {
                fetchGeolocation(imageType);
            } else {
                alert('Please select a valid image file.');
            }
        }

        function fetchGeolocation(imageType) {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(position => {
                    showPosition(position, imageType);
                }, showError);
            } else {
                alert('Geolocation is not supported by this browser.');
            }
        }

        function showPosition(position, imageType) {
            const latitude = position.coords.latitude;
            const longitude = position.coords.longitude;

            document.getElementById('latitude').value = latitude;
            document.getElementById('longitude').value = longitude;

            // Logic for handling different image types
            if (imageType === 'halfPhoto') {
                console.log(`Half Photo Location: Latitude: ${latitude}, Longitude: ${longitude}`);
            } else if (imageType === 'fullPhoto') {
                console.log(`Full Photo Location: Latitude: ${latitude}, Longitude: ${longitude}`);
            }
        }

        function showError(error) {
            switch(error.code) {
                case error.PERMISSION_DENIED:
                    alert("User denied the request for Geolocation.");
                    break;
                case error.POSITION_UNAVAILABLE:
                    alert("Location information is unavailable.");
                    break;
                case error.TIMEOUT:
                    alert("The request to get user location timed out.");
                    break;
                case error.UNKNOWN_ERROR:
                    alert("An unknown error occurred.");
                    break;
            }
        }
    </script>
</body>
</html>
