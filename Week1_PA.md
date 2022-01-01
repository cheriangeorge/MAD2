/*
 * calculateSimpleInterest calculates and returns the simple interest
 * (floor value) for a fixed deposit. Formula used is,

 * calculateSimpleInterest calculates and returns the simple interest
 * for a fixed deposit. Formula used is,
 * Simple Interest: P X R X T / 100
 *   where:
 *   P = Principal
 *   I = Daily interest rate
 *   N = Number of days
 *
 *  In case of any input error (wrong date format, alphabets in daily interest etc.), return -1
 *
 * @param {number} principal  - Principal amount
 * @param {number} dailyInterest  - daily interest rate
 * @param {string} startingDate  - Starting date of the fixed deposit in "YYYY-MM-DD" format, example "2015-03-25"
 * @param {string} endingDate  - Ending date of the fixed deposit in "YYYY-MM-DD" format, example "2015-03-25"
 * @return {number} interest
*/

/*
 * calculateCompoundInterest calculates and returns the compound interest
 * (floor value) for a fixed deposit. Formula used is,
 *   Compound Interest=P[(1+I/100)^N - 1]
 *   where:
 *   P = Principal
 *   I = Daily interest rate
 *   N = Number of days
 *
 *  In case of any input error (wrong date format, alphabets in daily interest etc.), return -1
 *
 * @param {number} principal  - Principal amount
 * @param {number} dailyInterest  - daily interest rate
 * @param {string} startingDate  - Starting date of the fixed deposit in "YYYY-MM-DD" format, example "2015-03-25"
 * @param {string} endingDate  - Ending date of the fixed deposit in "YYYY-MM-DD" format, example "2015-03-25"
 * @return {number} interest
*/

/*
 * extraAmountPercentage calculates and returns the extra amount percentage borrower will have to pay in case of
 * compound interest (floor value) in comparison to the simple interest for a fixed deposit.

 *  In case of any input error (wrong date format, alphabets in daily interest etc.), return -1
 *
 * @param {number} principal  - Principal amount
 * @param {number} dailyInterest  - Daily interest rate.
 * @param {string} startingDate  - Starting date of the fixed deposit in "YYYY-MM-DD" format, example "2015-03-25"
 * @param {string} endingDate  - Ending date of the fixed deposit in "YYYY-MM-DD" format, example "2015-03-25"
 * @return {number} percentage
*/

function calculateSimpleInterest(
  principal,
  dailyInterest,
  startingDate,
  endingDate
) {

// Add your code here
let s = new Date(startingDate);
let e = new Date(endingDate);
let d = e.getTime() - s.getTime();
let diff = d / (1000*60*60*24); // contains no of days
let interest = (principal * dailyInterest * diff)/100;
if (isNaN(interest)){
    return -1
}
return Math.floor(interest);

}

function calculateCompoundInterest(
  principal,
  dailyInterest,
  startingDate,
  endingDate
) {

// Add your code here
let s = new Date(startingDate);
let e = new Date(endingDate);
let d = e.getTime() - s.getTime();
let diff = d / (1000*60*60*24); // contains no of days
let interest = principal * (Math.pow((1+dailyInterest/100),diff)-1);
if (isNaN(interest)){
    return -1
}
return Math.floor(interest);

}

function extraAmountPercentage(
  principal,
  dailyInterest,
  startingDate,
  endingDate
) {

// Add your code here
let ans1 = calculateCompoundInterest(
  principal,
  dailyInterest,
  startingDate,
  endingDate
) ;
let ans2 = calculateSimpleInterest(
  principal,
  dailyInterest,
  startingDate,
  endingDate
);

let diff = ans1-ans2;
let percentage = diff / ans2 * 100;

if(ans1==-1 || ans2 ==-1 || isNaN(percentage)){
    return -1
}

return Math.floor(percentage);

}
