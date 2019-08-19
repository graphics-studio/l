//tracks running tally of values and operators prior to totalling
var tally = [];
//tracks current value prior to an operator being pressed
var currentValue = [];
var previousTotal = 0;
var total = 0;
var previousValue = "";
//tracks which operator was last pressed
var previousOper = "";
//tracks whether number is currently negative or positive
var sign = "positive";

//calculates total when an operator or equals is pressed
function calculate() {
  //case for very first calculation
  if (total === 0 && previousOper === "") {
    total = currentValue.join("");
    previousTotal = total;
    //cases for all remaining calculations
  } else if (previousOper == "/") {
    previousTotal = total;
    total = parseFloat(total) / parseFloat(currentValue.join(""));
  } else if (previousOper == "*") {
    previousTotal = total;
    total = parseFloat(total) * parseFloat(currentValue.join(""));
  } else if (previousOper == "-") {
    previousTotal = total;
    total = parseFloat(total) - parseFloat(currentValue.join(""));
  } else if (previousOper == "+") {
    previousTotal = total;
    total = parseFloat(total) + parseFloat(currentValue.join(""));
  }
}

//debug function
function debug() {
  console.log(
    "Prev Val: " +
      previousValue +
      " || Curr Val: " +
      currentValue.join("") +
      " || Tally: " +
      tally.join("") +
      " || Prev Total: " +
      previousTotal +
      " || Total: " +
      total +
      " || Prev Oper: " +
      previousOper +
      " || Sign: " +
      sign
  );
}

// used on(mousedown) rather than on(click) as it seemed to be more responsive with clickable divs
$(document).ready(function() {
  
  //digit inputs and decimal input
  $("#one").on("mousedown", function() {
    //case accounts for starting a new calc after totaling without clearing first
    if (previousOper == "=") {
      previousOper = "";
    }
    tally.push(1);
    currentValue.push(1);
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
    $("#result").html(currentValue);
  });
  
  $("#two").on("mousedown", function() {
    //case accounts for starting a new calc after totaling without clearing first
    if (previousOper == "=") {
      previousOper = "";
    }
    tally.push(2);
    currentValue.push(2);
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
    $("#result").html(currentValue);
  });
  
  $("#three").on("mousedown", function() {
    //case accounts for starting a new calc after totaling without clearing first
    if (previousOper == "=") {
      previousOper = "";
    }
    tally.push(3);
    currentValue.push(3);
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
    $("#result").html(currentValue);
  });
  
  $("#four").on("mousedown", function() {
    //case accounts for starting a new calc after totaling without clearing first
    if (previousOper == "=") {
      previousOper = "";
    }
    tally.push(4);
    currentValue.push(4);
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
    $("#result").html(currentValue);
  });
  
  $("#five").on("mousedown", function() {
    //case accounts for starting a new calc after totaling without clearing first
    if (previousOper == "=") {
      previousOper = "";
    }
    tally.push(5);
    currentValue.push(5);
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
    $("#result").html(currentValue);
  });
  
  $("#six").on("mousedown", function() {
    //case accounts for starting a new calc after totaling without clearing first
    if (previousOper == "=") {
      previousOper = "";
    }
    tally.push(6);
    currentValue.push(6);
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
    $("#result").html(currentValue);
  });
  
  $("#seven").on("mousedown", function() {
    //case accounts for starting a new calc after totaling without clearing first
    if (previousOper == "=") {
      previousOper = "";
    }
    tally.push(7);
    currentValue.push(7);
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
    $("#result").html(currentValue);
  });
  
  $("#eight").on("mousedown", function() {
    //case accounts for starting a new calc after totaling without clearing first
    if (previousOper == "=") {
      previousOper = "";
    }
    tally.push(8);
    currentValue.push(8);
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
    $("#result").html(currentValue);
  });
  
  $("#nine").on("mousedown", function() {
    //case accounts for starting a new calc after totaling without clearing first
    if (previousOper == "=") {
      previousOper = "";
    }
    tally.push(9);
    currentValue.push(9);
    // debug(previousValue, currentValue, tally, total, previousOper, sign);
    $("#result").html(currentValue);
  });
  
  $("#zero").on("mousedown", function() {
    //case accounts for starting a new calc after totaling without clearing first
    if (previousOper == "=") {
      previousOper = "";
    }
    tally.push(0);
    currentValue.push(0);
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
    $("#result").html(currentValue);
  });
  
  $("#decimal").on("mousedown", function() {
    //case accounts for starting a new calc after totaling without clearing first
    if (previousOper == "=") {
      previousOper = "";
    }
    //prevents multiple decimals in a row
    if (currentValue[currentValue.length - 1] == ".") {
      return;
      //if decimal or negative is selected first, adds preceding 0 for formatting
    } else if (currentValue.length === 0 || currentValue[0] === "-") {
      tally.push("0");
      tally.push(".");
      currentValue.push("0");
      currentValue.push(".");
      //default behavior
    } else {
      tally.push(".");
      currentValue.push(".");
    }
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
    $("#result").html(currentValue);
  });

  //operators
  $("#divide").on("mousedown", function() {
    //allows switching current operator to divide
    if (
      (previousOper == "*" || previousOper == "-" || previousOper == "+") &&
      tally[tally.length - 1].length > 2
    ) {
      tally.splice(tally.length - 1, 1, " / ");
      previousOper = "/";
      //allows dividing immediately after a total
    } else if (previousOper == "=") {
      tally.push(previousTotal);
      tally.push(" / ");
      previousValue = previousTotal;
      total = previousTotal;
      previousOper = "/";
      //prevents multiple divide operations or divide being selected as first button
    } else if (
      (previousOper == "/" && tally[tally.length - 1] == " / ") ||
      (previousTotal === 0 && tally.length === 0)
    ) {
      return;
      //default behavior
    } else {
      tally.push(" / ");
      previousValue = currentValue.join("");
      calculate(total, previousOper, currentValue);
      previousOper = "/";
    }
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
    currentValue.length = 0;
    sign = "positive";
    $("#tally").html(tally);
    $("#result").html("/");
  });
  
  $("#multiply").on("mousedown", function() {
    //allows switching current operator to multiply
    if (
      (previousOper == "/" || previousOper == "-" || previousOper == "+") &&
      tally[tally.length - 1].length > 2
    ) {
      tally.splice(tally.length - 1, 1, " * ");
      previousOper = "*";
      //allows multiplying immediately after a total
    } else if (previousOper == "=") {
      tally.push(previousTotal);
      tally.push(" * ");
      previousValue = previousTotal;
      total = previousTotal;
      previousOper = "*";
      //prevents multiple multiply operations or multiply being selected as first button
    } else if (
      (previousOper == "*" && tally[tally.length - 1] == " * ") ||
      (previousTotal === 0 && tally.length === 0)
    ) {
      return;
      //default behavior
    } else {
      tally.push(" * ");
      previousValue = currentValue.join("");
      calculate(total, previousOper, currentValue);
      previousOper = "*";
    }
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
    currentValue.length = 0;
    sign = "positive";
    $("#tally").html(tally);
    $("#result").html("*");
  });
  
  $("#subtract").on("mousedown", function() {
    //allows switching current operator to subtract
    if (
      (previousOper == "/" || previousOper == "*" || previousOper == "+") &&
      tally[tally.length - 1].length > 2
    ) {
      tally.splice(tally.length - 1, 1, " - ");
      previousOper = "-";
      //allows subtracting immediately after a total
    } else if (previousOper == "=") {
      tally.push(previousTotal);
      tally.push(" - ");
      previousValue = previousTotal;
      total = previousTotal;
      previousOper = "-";
      //prevents multiple subtract operations or subtract being selected as first button
    } else if (
      (previousOper == "-" && tally[tally.length - 1] == " - ") ||
      (previousTotal === 0 && tally.length === 0)
    ) {
      return;
      //default behavior
    } else {
      tally.push(" - ");
      previousValue = currentValue.join("");
      calculate(total, previousOper, currentValue);
      previousOper = "-";
    }
    // debug(previousValue, currentValue, tally, total, previousOper, sign);
    currentValue.length = 0;
    sign = "positive";
    $("#tally").html(tally);
    $("#result").html("-");
  });
  
  $("#add").on("mousedown", function() {
    //allows switching current operator to addition
    if (
      (previousOper == "/" || previousOper == "*" || previousOper == "-") &&
      tally[tally.length - 1].length > 2
    ) {
      tally.splice(tally.length - 1, 1, " + ");
      previousOper = "+";
      //allows adding immediately after a total
    } else if (previousOper == "=") {
      tally.push(previousTotal);
      tally.push(" + ");
      previousValue = previousTotal;
      total = previousTotal;
      previousOper = "+";
      //prevents multiple add operations or adds being selected as first button
    } else if (
      (previousOper == "+" && tally[tally.length - 1] == " + ") ||
      (previousTotal === 0 && tally.length === 0)
    ) {
      return;
      //default behavior
    } else {
      tally.push(" + ");
      previousValue = currentValue.join("");
      calculate(total, previousOper, currentValue);
      previousOper = "+";
    }
    // debug(previousValue, currentValue, tally, total, previousOper, sign);
    currentValue.length = 0;
    sign = "positive";
    $("#tally").html(tally);
    $("#result").html("+");
  });
  
  $("#equals").on("mousedown", function() {
    //prevents totalling when last button was an operator
    if (
      (previousOper == "/" ||
        previousOper == "*" ||
        previousOper == "-" ||
        previousOper == "+") &&
      tally[tally.length - 1].length > 1
    ) {
      return;
      //prevents first button being the equals button
    } else if (previousTotal === 0 && tally.length === 0) {
      return;
      //default totalling behavior
    } else if (previousOper !== "=") {
      calculate(total, previousOper, currentValue);
      tally.push(" = " + total);
      $("#result").html(total);
      $("#tally").html(tally);
    }
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
    //resets all the variable and tracks total as previousTotal
    tally.length = 0;
    currentValue.length = 0;
    sign = "positive";
    previousTotal = total;
    total = 0;
    previousValue = 0;
    previousOper = "=";
  });

  //special operators
  //clears all variables and resets calculator
  $("#clear").on("mousedown", function() {
    tally.length = 0;
    currentValue.length = 0;
    total = 0;
    previousTotal = 0;
    previousValue = 0;
    previousOper = "";
    sign = "positive";
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
    $("#tally").html(0);
    $("#result").html(0);
  });
  
  //deletes items from current value and tally...if no current value, no action is performed
  $("#delete").on("mousedown", function() {
    //case for when current value is greater than 1 character
    if (currentValue.length > 1) {
      tally.pop();
      currentValue.pop();
      $("#result").html(currentValue);
      //case for when current value has only 1 character
    } else if (currentValue.length == 1) {
      //cases to handle formatting of tally
      if (tally.length > 1) {
        tally.pop();
      } else {
        tally.length = 0;
      }
      currentValue.length = 0;
      $("#result").html(0);
    }
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
  });
  
  //changes between negative and positive numbers
  $("#sign").on("mousedown", function() {
    //prevents changing sign when last button was an operator
    if (
      tally[tally.length - 1] == " / " ||
      tally[tally.length - 1] == " * " ||
      tally[tally.length - 1] == " - " ||
      tally[tally.length - 1] == " + " ||
      tally[tally.length - 1] == " = "
    ) {
      return;
      //changing sign to negative
    } else if (sign === "positive") {
      sign = "negative";
      //case for when current value has at least one digit
      if (currentValue.length > 0) {
        currentValue.splice(0, 0, "-");
        for (var i = tally.length - 1; i >= 0; i--) {
          //case for when running tally has more than one value, changes sign on the most recent value only
          if (tally[i].length > 1) {
            tally.splice(i + 1, 0, "-");
            break;
            //case for when running tally has only one value
          } else if (i === 0) {
            tally.splice(0, 0, "-");
          }
        }
        //case for when current value and running tally are null (sign is first digit pressed)
      } else if (currentValue.length === 0 && tally.length === 0) {
        currentValue.splice(0, 0, "-");
        tally.splice(0, 0, "-");
        //case for when current value is null, but running tally is not
      } else if (currentValue.length === 0) {
        currentValue.splice(0, 0, "-");
      }
      $("#result").html(currentValue.join(""));
      //changing sign to positive
    } else if (sign === "negative") {
      sign = "positive";
      //case for when current value has at least one digit
      if (currentValue.length > 1) {
        currentValue.splice(0, 1);
        //removes negative sign on running tally
        for (var t = tally.length - 1; t >= 0; t--) {
          if (tally[t] == "-") {
            tally.splice(t, 1);
            break;
          }
          $("#result").html(currentValue.join(""));
        }
        //case for when negative was the first button pressed
      } else if (
        currentValue.length === 1 &&
        currentValue[0] == "-" &&
        tally.length === 1 &&
        tally[0] == "-"
      ) {
        currentValue.splice(0, 1);
        tally.splice(0, 1);
        $("#result").html(0);
      }
    }
    // debug(previousValue,currentValue,tally,total,previousOper,sign);
  });
});
