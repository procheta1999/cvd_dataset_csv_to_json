# csv-to-json-converter for CVD dataset
A shell script that converts CVD dataset csv file to its corresponding json file

__Tested in Windows__   
-----

# INSTRUCTIONS: 
1. Firstly, git bash into your folder where you have kept the .sh files.  
2. copy the csv file (input.csv) into the folder (csd-json) with csvtojson.sh file
3. execute first "chmod a+x csvtojson.sh" to make csvtojson.sh executable 
4. execute the csvtojson.sh file in the Git Bash terminal with "bash ./csvtojson.sh input.csv > output.json" 
5. output.json will contain the JSON format of the CVD dataset. 

****

# Basic documentation of the work:
1. First I downloaded the dataset from [CVD Dataset](https://www.kaggle.com/aiaiaidavid/cardio-data-dv13032020) .
<br>
Here the data is hude, so for convenience, first 8225 rows have only been considered.
2. Next, for converting to JSON file:
- csvtojson.sh : It reads the csv files line by line and takes the table headers as the keys of the objects in the json array 'data' and the data of the table as the value of each set of keys.
<br>
Example: Suppose in line 2 of the csv file (since line 1 of the csv file contains the table headers) there are: 
<br>
50,2,168,62,110,80,1,1,0,0,1,0
<br>
<br>
So while converting to json, it will appear almost like this : 
<br>
{
    <br>
"data":
<br>
[
    <br>
{
    <br>
   "AGE":"50",
   <br>"GENDER":"2",
   <br>"HEIGHT":"168",
   <br>"WEIGHT":"62",
   <br>"AP_HIGH":"110",
   <br>"AP_LOW":"80",
   <br>"CHOLESTEROL":"1",
   <br>"GLUCOSE":"1",
   <br>"SMOKE":"0",
   <br>"ALCOHOL":"0",
   <br>"PHYSICAL_ACTIVITY":"1",
   <br>"CARDIO_DISEASE":"0"
<br>},
<br>
...............
<br>
}
<br>]
<br>

## Explanantion of the code:
<code>input=$1</code>
<br>Takes input parameter<br>
<code>[ -z $1 ]</code><br>
<br>Checks if input[1] is empty or not
<code>[ ! -e $input ]</code><br>
Checks for existence of filename(input)<br>
<code>read first_line < $input</code><br>
Reads first line of input file and stores it in first_line<br>
<code>attributes=`echo $first_line | awk -F, {'print NF'}`</code><br>
echo $first_line | awk -F, {'print NF'} with tail tags acts as a Bash command where:

1. awk for pattern scanning and processing
2. awk -F fs: where fs is the input seperator
3. NF is the count of input fields.
<br>

So basically, this command returns the number of fields in the input file.