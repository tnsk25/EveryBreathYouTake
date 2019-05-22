# EveryBreathYouTake-WebVisualisation
The application analyses the Air Quality data for different states and counties across the US from 1990-2018. 
The Air Quality data has been categorized into Annual, Daily, Hourly data files. The application analyses the 
same data in multiple ways (Pie Chart, Bar Chart, Line Chart, HeatMap, Table) to derive insights from the 
changing trends over the years. Apart from analysing the Air Quality for the US, this application also 
analyses the Air Quality data for Hong Kong as well. We have experimented with different layouts 
considering user experience as well.

Libraries Used:
shiny
shinydashboard 
ggplot2 
lubridate 
DT 
grid 
leaflet 
scales
shinycssloaders
shinyWidgets
tidyverse 
tmap 
tmaptools 
sf 
splitstackshape 
cdlTools 
plotly 

The data was collected from the US EPA website. You can download all the Annual, Daily, Hourly data files from https://aqs.epa.gov/aqsweb/airdata/download_files.html
The data files for Hong Kong can be downloaded from https://openaq.org/#/countries 
The data files for all Heatmaps can be downloaded from https://www.census.gov/geo/maps-data/data/cbf/cbf_counties.html 

The Data preprocessing for this application is done for Daily and Hourly Data of the United States. 
Apart from this preprocessing was done separately for Hong Kong data. 
In the daily data, all the daily files from 1990 to 2018 were loaded and only necessary columns 
were selected and removing the State.Code, County.Code, Defining.Site and Number.of.Sites.Reporting 
columns which are not used for this application. This preprocessing helped us reduce the daily files 
size from 650 MB (approx.) to 400 MB (approx.). 
Now, coming to the hourly data for 2018. We had 8 huge separate files for each pollutant, Wind 
and Temperature data. The first step of this data preprocessing is the extraction of dates with 
respect to the county from all the files so that we can develop the functionality to show the user 
which data is available for the selected County and date under hourly section. We extracted the date 
from 18 individual files and compiled into a single file. 
After this, for plotting purpose we had done some preprocessing since we cannot load such huge files 
into application directly. So we took each file separately and divided into 12 files based on the month. 
During this process, we removed the columns in the data which are not required for the application. Also, 
the values were converted into a single unit for a common scale. Then, we calculated the respective imperial 
units for the values (ppm to mg/m3).
Then, for plotting the heat map we needed the data for the pollutants at a daily level. So we used the 
preprocessed file from the above step and used that to calculate the daily value of the pollutants by 
aggregating the hourly values given to a single value for that day. We made 12 separate files monthly vise for the map data.
We had the hourly files for the Hong Kong data for 6 pollutants for 16 locations for the last 90 days. 
We made a separate file for the latitude and longitude files for the 16 locations. After that, we removed 
the columns not used in the application from the hourly data and saved that for the hourly plotting. Then 
for the daily and monthly plotting, we aggregated these hourly values to a daily and monthly format.
For these preprocessed files we'll need to run the preprocessing code. Please follow the below folder structure while running the preprocess code.
Raw Files/Daily --> Place the daily raw files for the US here
Raw Files/Monthly --> Place the Monthly files for the US here
Raw Files/Hong Kong --> Place the Individual pollutant file here
Place the preprocess.R files one folder level above the Raw Files directory and the preprocessed files 
will be generated. This may take up to 10 to 15 minutes of time.
