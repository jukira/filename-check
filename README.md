
<!DOCTYPE html>
<html>
<body>

<p><strong>Check your filenames</strong></p>

<p>Copy and paste the filename you want to check in the box, click check.<br/>
Characters included in the search and replace are:<br/>
<strong>śćóęążźáéíóúüñ¿¡.!@#$%^*+  - case insensitive</strong>

</p>

<input id="userInput">


<button onclick="displayResults()">Check</button>

<p id="result"></p>
</br>
<p id="description"></p>
<p id="finalresult"></p>

<script>

function replaceAll(str, find, replace) {
  	return str.replace(new RegExp(find, 'g'), replace);
}

function convertToCorrectString(correctArray) {
	//* THIS IS UGLY BUT FUNCTIONING CODE
	var stringWithComas = correctArray.toString();
    var stringWithSpecialChars = replaceAll(stringWithComas, "," , "");
    var stringAlmostReady = replaceAll(stringWithSpecialChars, (/[¿¡.!@#$%^&*+"]+/i) , "");
    var stringReady = replaceAll(stringAlmostReady, " " , "_");
    
    return stringReady;
}

function searchForMatch (){
	var userInputArray = convertToString();
    var wrongArray = ["ś","ć","ó","ę","ą","ż","ź","á","é","í","ó","ú","ü","ñ"];
    var correctArray = ["s","c","o","e","a","z","z","a","e","i","o","u","u","n"];
    
    for (var i = 0; i < userInputArray.length; i++) {
        for (var j = 0; j < wrongArray.length; j++) {  	
        	if (userInputArray[i] == wrongArray[j]) {
                userInputArray[i] = correctArray[j];
            }
        	};
    }
    var finalString = convertToCorrectString(userInputArray);
    return finalString;
    }
    
    
function convertToString () {
	var input = document.getElementById("userInput").value; 
    var str = input.toLowerCase();
    var userInputArray = [];
    
     for (var i = 0; i < str.length; i++){
    	var character = str.charAt(i);
        userInputArray.push(character);
    	};
    
    return userInputArray;
	}


function checkIfContains (str) {
	var foundedWrongChars = [];
    for (var i = 0; i < str.length; i++){
    	var n = str.charAt(i);
        var m = n.search(/[śćóęążźáéíóúüñ¿¡.!@#$%^&*+ "]+/i);
        if (m > -1){
        foundedWrongChars.push(n);
        }
    	};
	return foundedWrongChars;

}

function displayResults() {
    var str = document.getElementById("userInput").value; 
    var communicate;
    var foundedWrongChars = checkIfContains(str);
    var description = "The corrected version of your filename to copy:"
    
    if (foundedWrongChars.length){
    	communicate = "The following special characters were found: " + foundedWrongChars;
        var finalResult = searchForMatch();
    	document.getElementById("finalresult").innerHTML = finalResult;
        document.getElementById("description").innerHTML = description;
    	}
        else{
        communicate = "Go ahead the filename is safe :)";
        };
        
    document.getElementById("result").innerHTML = communicate;
    
}


</script>

</body>
</html>
