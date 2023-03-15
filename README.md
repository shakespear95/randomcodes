# randomcodes

<!DOCTYPE html>
<html>
<head>
	<title>Local Storage Example</title>
</head>
<body>

	<h1>Input Section</h1>
	<form>
		<label for="name">Name:</label>
		<input type="text" id="name" name="name"><br><br>

		<label for="email">Email:</label>
		<input type="email" id="email" name="email"><br><br>

		<input type="button" value="Add" onclick="addData()">
	</form>

	<h1>Output Section</h1>
	<div id="output"></div>

	<script>
		// Retrieve data from local storage or create an empty array if no data exists
		var data = JSON.parse(localStorage.getItem("data")) || [];

		// Add input data to the data array and update local storage and display data
		function addData() {
			var name = document.getElementById("name").value;
			var email = document.getElementById("email").value;

			data.push({ name: name, email: email });
			localStorage.setItem("data", JSON.stringify(data));

			displayData();
		}

		// Remove a specific set of input data from the data array by its index, update local storage and display data
		function removeData(index) {
			data.splice(index, 1);
			localStorage.setItem("data", JSON.stringify(data));

			displayData();
		}

		// Display all stored input data in the output section
		function displayData() {
			var output = document.getElementById("output");
			output.innerHTML = "";

			if (data.length > 0) {
				for (var i = 0; i < data.length; i++) {
					var dataItem = data[i];

					// Create a container div for each set of input data
					var dataContainer = document.createElement("div");
					dataContainer.classList.add("data-container");

					// Create a span element for the name output and set its text content
					var nameOutput = document.createElement("span");
					nameOutput.classList.add("name-output");
					nameOutput.textContent = "Name: " + dataItem.name;

					// Create a span element for the email output and set its text content
					var emailOutput = document.createElement("span");
					emailOutput.classList.add("email-output");
					emailOutput.textContent = "Email: " + dataItem.email;

					// Create an input element for the remove button, set its attributes, and add a click event listener to call the removeData function with the current index as an argument
					var removeButton = document.createElement("input");
					removeButton.classList.add("remove-button");
					removeButton.setAttribute("type", "button");
					removeButton.setAttribute("value", "Remove");
					removeButton.setAttribute("data-index", i); // add a data-index attribute with the current index value
					removeButton.addEventListener("click", function() {
						var index = this.getAttribute("data-index"); // get the data-index value from the clicked button
						removeData(index);
					});

					// Append the name output, email output, and remove button to the data container div
					dataContainer.appendChild(nameOutput);
					dataContainer.appendChild(emailOutput);
					dataContainer.appendChild(removeButton);

					// Append the data container div to the output section
					output.appendChild(dataContainer);
				}
			} else {
				output.textContent = "No data stored in local storage";
			}
		}

		// Display any stored input data on page load
		displayData();
	</script>

</body>
</html>
