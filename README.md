# EmailAutomation

   This is a python program for sending bulk emails automatically . It is developed for the billing department of BSNL for automatically mailing the monthly bills.
   The program uses the gmail server to do so. The input to the program is email id , password and body of the email.
It asks for path of the directory containing the ps files and the path of the csv file having the email ids and the account numbers of the customers.
	  The program takes the account number from the csv file and searches for the ps file whoes name matches with that account number in the directory having the ps files. It then attaches the ps file to the email id corresponding to that account number in the csv file.The program also logs the list of account numbers and email ids of the the sent emails with the time and date on which the mails were sent in a file for future reference.
	   The mail is sent by the given email id and body to all the customers whoes account numbers are present in the csv file.
Apart from the error message of gmail on finding incorrect reciever email id which is sent to the senders id,the program also prints the list of account numbers which are present in the csv but their ps files are not available . 
	

