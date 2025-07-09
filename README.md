# Is YOUR ocean temperature rising?

The goal of this assignment is to use publicly available data to refute or to validate the claim that
ocean temperatures are rising. While vast amounts of data is available, our ability to consume
all that data is neither practical nor essential for our purposes. So we will get to our conjecture
by taking very simple steps. The overall flow is outlined below - the accompanying code
structure mimics this :

[While APIs may exist to dynamically download netCDF data in bulk, there is concern that some
of the memory issues you ran into may be related to that process. If you are successful with an
API that is fine; else please use the following manual steps in 1.0]

**1.0 Download/Store Data:**
- Pick an anchor date: It can be your birthdate, or any other date. I chose January 1 as my
anchor date.
- Go to the Copernicus website and for your assigned sea, download, MANUALLY, all the
datasets for that specified single-day. For my example it was 1980-Jan-1,
1981-Jan-1.....2023-Jan-1, 2024-Jan-1. This is the most cumbersome/manual process. Again,
you may find another way to do this and that is fine.
- I recommend that you store it in a separate folder in your Google Drive.
- Set the folder as the ‘base_path’, so that each file can further be loaded using iteratively.
  
**2.0 Load Data:**
Load one dataset so that you can check the dimensions, variables and the range of the
coordinates. The generate_file_paths function is an easy way to “mark” or “label” the
downloaded data. This will help us iterate through each file during the subsequent load_netCDF
function.
[3.0 and 4.0 refer to steps needed to extract sea-surface-temperatures for each year and to
store them in a data frame. This can be done in your own way, if you wish]

**3.0 Get sea-surface-temperature for a specified lat-long:**
The extract_sst_data function iterates through the file-paths and gets the sst in that file for a
specified lat-long. I have provided a utility function find_nearest as exact matches of your
lat-long may not always be available [if interested in the practical side of ocean data collection,
please research moorings and drifters]
![image](https://github.com/user-attachments/assets/c8adf09b-da95-49aa-a2b3-57497cf2e5bd)


**4.0 Create single data frame (and optimally write out as csv):**
The process_years function loops through each of the file_paths (each of the years), gets the
corresponding sst and creates a single data frame. This can be written out to a csv (and
subsequently read back in), especially if you incur memory issues..

**5.0 Plot data and visualize:**
Using any number of available plotting tools (e.g. pyplot) plot the data you have extracted. The
x-axis should be the year and the y-axis the sst.

**6.0 Train, predict and report MAPE:**

Using all but the most recent 4 data points, train a simple linear model and predict four periods
(years) out. Use the test data points (4 of them) to quantify model accuracy using the MAPE
measure. In my case I trained 1982-Jan-1 to 2020-Jan-1 and tested the predictions against sst
data for 2021-Jan-1 through 2024-Jan-1.

Please ensure that the test data is NOT included in your training data.

Reference: https://data.marine.copernicus.eu/product/SST_MED_SST_L4_REP_OBSERVATIONS_010_021/description
