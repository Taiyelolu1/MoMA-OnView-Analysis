# MoMA OnView Analysis
This research dataset contains 157,630 records, representing all of the works that have been accessioned into MoMA’s collection and cataloged in their database. It includes basic metadata for each work, including title, artist, date made, medium, dimensions, and date acquired by the Museum. This project focuses on the artworks currently on display at the museum (MoMA OnView). The dataset used for this project was sourced from [Maven Analytics Playground](https://mavenanalytics.io/data-playground).
## Project Bacground
The Museum of Modern Art (MoMA) is an art museum located in Midtown Manhattan, New York City, on 53rd Street between Fifth and Sixth Avenues. MoMA's collection spans the late 19th century to the present, and includes over 200,000 works of architecture and design, drawing, painting, sculpture, photography, prints, illustrated and artist's books, film, as well as electronic media.

The museum has been instrumental in shaping the history of modern art, particularly modern art from Europe. In recent decades, MoMA has expanded its collection and programming to include works by traditionally underrepresented groups. The MoMA Library includes about 300,000 books and exhibition catalogs, more than 1,000 periodical titles and more than 40,000 files of ephemera about individual artists and groups. The archives hold primary source material related to the history of modern and contemporary art. In 2023, MoMA was visited by over 2.8 million people, making it the 15th most-visited art museum in the world and the 6th most-visited museum in the United States.

## Overview of the Data
The data contained two tables; Artists and Artworks. The data was `cleaned` and `transformed` using the `Power Query Editor` in Power BI. The major transformations carried out in the Power Query Editor inlcude:
* Removal of unwanted columns: Columns that were found to be unuseful for the analysis were removed so as to focus on the ones needed.
* Renaming Columns: Some columns were also renamed for easy understanding in the course of the project.
* Replacing values: Columns with blank rows were replaced with "Unknown" or "null".
* Formatting columns: Records in the columns were given proper data types, trimmed, and given proper casing to give a better uniform look of the tables.
* Added column: Added a custom column `Year` by extracting the first four digit from the `Date` column.

After cleaning, the columns left in both tables include:

**Artists**
* ConstituentID: A unique identifier for the artist in the museum's database system.
* ArtistName: The public display name of the artist, which may be their full name, pseudonym, or stage name.
* ArtistBio: A short biography or background information about the artist. 
* Nationality: The country or region the artist is originally from. 
* Gender: The gender of the artist.
* BirthDate: The birth year of the artist.
* DeathDate: The death year of the artist.

**Artworks**
* ObjectID: A unique identifier for the artwork in the MoMA database system.
* Title: The name or title of the artwork
* ConstituentID: Unique identifier(s) for the artist(s) related to the artwork (separated by commas).
* Year: Year the artwork was created. 
* Medium: The material(s) used to create the artwork, such as oil paint, marble, video or other mediums.
* Dimensions: The size or physical dimensions of the artwork (e.g., height x width x depth in cm).
* Classification: The classification of the artwork, such as painting, sculpture, drawing, photography etc.
* Department: The department of the museum where the artwork is stored or categorized. 
* DateAquired: The date the artwork was acquired by the museum. 
* URL: A web link to more detailed information about the artwork on the MoMA website. 
* ImageURL: The URL of the image of the artwork, hostedby the museum. 
* OnView: Location of the artwork if it is currently on display in the museum (otherwise blank).

***The CSV files and scripts generated from the Power Query Editor have been included in the repository for this project.***

## Tools used 
1. **Power BI**: This was the major tool used in this project. Power BI was used in creating the `visualization` and report for the insights generated from this project. Power BI service, a component of Power BI was also utilized in creating a web link that allows interactivity and navigation with the report.
2. **Power Query Editor**: This is an advanced feature of Power BI that allows transformation to be carried out on a dataset. The `Power Query Editor` was used in carrying out transformations across different columns such as adding custom columns, formatting columns, replacing values, etc.

## Project Workflow
A Project Workflow provides a good structure for every data analytics project. It helps to establish a clear roadmap of sequential steps from the initial problem to the final insights. This keeps the project organized and aligned with goals. It also outlines tasks within each project phase, preventing important elements from being overlooked and making the process more efficient. The workflow for this project includes:
1. Project objective.
2. Data collection.
3. Data cleaning and preparation.
4. Data analysis and visualization.
5. Interpretation and reporting.

## Project Objective
This project was aimed at focusing on the analysis of artworks which are currently in display at MoMa. Insights about the artists featured, the number of artworks they have done, the types of artworks in the museum etc., can be gotten from this analysis. Power BI was used to provide interactive dashboards that support data-driven insights and strategic decision-making.

## Data Collection 
The data for this project was collected from [Maven Analytics Playground](https://mavenanalytics.io/data-playground). The data included records of various artists, their artworks, date of aquisition by the museum and much more. 
## Data Cleaning & Preparation
The data cleaning process was done using the Power Query Editor in Power BI. Some major operations such as removal of unwanted columns were done and other text operations such as capitalising, trimming, and replacing values were also carried out on some columns. The [M Query Codes] from the Power Query Editor have been attached to this repository. Please note that the Power Query Editor automatically writes/generates these codes based on the steps applied in the editor.

After data cleaning, a new column `Year` was created by extracting the first four (4) digits from the `Date` column. I made sure `Date` was first in the tetx datatype to make the extraction possible. Another major step taken was creating a bridge table `ArtworkArtists` so that each artist-arwork pairing has its own row. The various steps taken to achieve this include:

* Duplicated the `Artworks` table, keeping only columns; `ObjectID`, `Title`, `ConstituentID`, `Year` and `DateAquired`.
* Reordered the columns and change the table name to `ArtworkArtists`.
* Splitted the `ConstituentID` column by delimiter comma (,) into rows and changed the datatype to whole number.  

These were all done in the Power Query Editor. 

Outside Power Query Editor, a `DateTable` was created using the minimum and maximum date from the `DateAquired`. The table contained columns for `Date`, `year`, `Month`, `Month Number`, and `Quarter`. This table was marked as the date table. A new relationship was then created between the `DateTable` and the `DateAquired`. 

In addition, I created new measures and new columns to provide in-depth insights into the various records. Some of these measures and columns include:



