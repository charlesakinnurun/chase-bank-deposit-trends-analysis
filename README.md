
<!--------------------------------------------------------------------------------------------------------------------------------------------------------------------->

<!-- ![header](/assets/chase_bank_header.png)-->

![header](/assets/jpmorgan_header.png)

<h1 align="center">Chase Bank Deposits Trends Analysis</h1>

<!---------------------------------------------------------------------------------------------------------------------------------------------------------------------->

<p>What I learned</p>

-   How to clean and preprocess messy tabular data (fill missing values, convert dates, standardize column names).
-   How to write SQL queries for aggregation (SUM, AVG, COUNT) and filtering (WHERE, LIKE, GROUP BY).
-   How to interpret deposit trends across states, counties, and time (growth between 2010–2016).


<p> What I did</p>

-   Loaded the raw branch deposit dataset and cleaned it (handled missing values, converted dates, renamed columns).
-   Built a SQL schema and table for the cleaned data.
-   Ran analysis queries to answer questions about top states, branches, growth trends, and branch counts.

<!----------------------------------------------------------------------------------------------------------------------------------------------------------------------->


<h2 align="center">Workflow</h1>

<!----------------------------------------------------------------------------------------------------------------------------------------------------------------------->

- Data Collection

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }

        .dataframe tbody tr th {
            vertical-align: top;
        }

        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
    <thead>
        <tr style="text-align: right;">
        <th></th>
        <th>Institution Name</th>
        <th>Main Office</th>
        <th>Branch Name</th>
        <th>Branch Number</th>
        <th>Established Date</th>
        <th>Street Address</th>
        <th>City</th>
        <th>County</th>
        <th>State</th>
        <th>Zipcode</th>
        <th>Latitude</th>
        <th>Longitude</th>
        <th>2010 Deposits</th>
        <th>2011 Deposits</th>
        <th>2012 Deposits</th>
        <th>2013 Deposits</th>
        <th>2014 Deposits</th>
        <th>2015 Deposits</th>
        <th>2016 Deposits</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <th>0</th>
        <td>JPMorgan Chase Bank</td>
        <td>1</td>
        <td>JPMorgan Chase Bank Main Office</td>
        <td>0</td>
        <td>01/01/1824</td>
        <td>1111 Polaris Parkway</td>
        <td>Columbus</td>
        <td>Delaware</td>
        <td>OH</td>
        <td>43240</td>
        <td>40.14453</td>
        <td>-82.99115</td>
        <td>633131000.0</td>
        <td>743268000.0</td>
        <td>832455000.0</td>
        <td>916543000.0</td>
        <td>1.032549e+09</td>
        <td>1.069425e+09</td>
        <td>1155185000</td>
        </tr>
        <tr>
        <th>1</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Vernon Hills Scarsdale Branch</td>
        <td>2</td>
        <td>3/20/1961</td>
        <td>676 White Plains Road</td>
        <td>Scarsdale</td>
        <td>Westchester</td>
        <td>NY</td>
        <td>10583</td>
        <td>40.97008</td>
        <td>-73.80670</td>
        <td>293229.0</td>
        <td>310791.0</td>
        <td>325742.0</td>
        <td>327930.0</td>
        <td>3.277920e+05</td>
        <td>3.414750e+05</td>
        <td>381558</td>
        </tr>
        <tr>
        <th>2</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Great Neck Northern Boulevard Branch</td>
        <td>3</td>
        <td>9/9/1963</td>
        <td>410 Northern Boulevard</td>
        <td>Great Neck</td>
        <td>Nassau</td>
        <td>NY</td>
        <td>11021</td>
        <td>40.77944</td>
        <td>-73.72240</td>
        <td>191011.0</td>
        <td>206933.0</td>
        <td>216439.0</td>
        <td>237983.0</td>
        <td>2.341830e+05</td>
        <td>2.624550e+05</td>
        <td>278940</td>
        </tr>
        <tr>
        <th>3</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>North Hartsdale Branch</td>
        <td>4</td>
        <td>2/19/1966</td>
        <td>353 North Central Avenue</td>
        <td>Hartsdale</td>
        <td>Westchester</td>
        <td>NY</td>
        <td>10530</td>
        <td>41.02654</td>
        <td>-73.79168</td>
        <td>87110.0</td>
        <td>88367.0</td>
        <td>93163.0</td>
        <td>109659.0</td>
        <td>1.119850e+05</td>
        <td>1.167720e+05</td>
        <td>140233</td>
        </tr>
        <tr>
        <th>4</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Lawrence Rockaway Branch</td>
        <td>5</td>
        <td>1/16/1965</td>
        <td>335 Rockaway Turnpike</td>
        <td>Lawrence</td>
        <td>Nassau</td>
        <td>NY</td>
        <td>11559</td>
        <td>40.62715</td>
        <td>-73.73675</td>
        <td>172608.0</td>
        <td>172749.0</td>
        <td>189413.0</td>
        <td>198445.0</td>
        <td>2.051980e+05</td>
        <td>2.232000e+05</td>
        <td>235594</td>
        </tr>
        <tr>
        <th>...</th>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        </tr>
        <tr>
        <th>5408</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Alameda and Compton Blvd Branch</td>
        <td>7981</td>
        <td>11/3/2015</td>
        <td>251 E Compton Blvd</td>
        <td>Compton</td>
        <td>Los Angeles</td>
        <td>CA</td>
        <td>90220</td>
        <td>33.89601</td>
        <td>-118.22084</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>3446</td>
        </tr>
        <tr>
        <th>5409</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Charleston and Rancho</td>
        <td>7982</td>
        <td>2/2/2016</td>
        <td>2311 W Chafrleston Blvd</td>
        <td>Las Vegas</td>
        <td>Clark</td>
        <td>NV</td>
        <td>89102</td>
        <td>36.14270</td>
        <td>-115.19043</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>2666</td>
        </tr>
        <tr>
        <th>5410</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Los Olivos Branch</td>
        <td>7984</td>
        <td>3/15/2016</td>
        <td>8593 Irvine Center Drive</td>
        <td>Irvine</td>
        <td>Orange</td>
        <td>CA</td>
        <td>92618</td>
        <td>33.64412</td>
        <td>-117.74453</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>6689</td>
        </tr>
        <tr>
        <th>5411</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Lake Forest Branch</td>
        <td>7988</td>
        <td>1/1/2016</td>
        <td>5660 Read Blvd</td>
        <td>New Orleans</td>
        <td>Orleans</td>
        <td>LA</td>
        <td>70127</td>
        <td>30.03205</td>
        <td>-89.97260</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>94133</td>
        </tr>
        <tr>
        <th>5412</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Buffalo-Mm Branch</td>
        <td>7989</td>
        <td>1/1/2016</td>
        <td>350 Main Street</td>
        <td>Buffalo</td>
        <td>Erie</td>
        <td>NY</td>
        <td>14202</td>
        <td>42.88429</td>
        <td>-78.87487</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>45596</td>
        </tr>
    </tbody>
    </table>
    <p>5413 rows × 19 columns</p>
    </div>

<!------------------------------------------------------------------------------------------------------------------------------------------------------------------->

- <h4><a href="/scipt/cleaning.py">Data Preprocessing</a></h4>

    - Data Loading
    - Fill missing "Acquired Data" values with "Not Acquired"
    - Drop rows with missing Latitude or Longitude
    - List of deposit columns with missing values
    - Fill missing values in deposit columns with 0
    - Convert "Established Date" to datetime objects
    - Convert "Acquired Date" to datetime objects, handling the "Not Acquired" string
    - Rename columns for consistency
    - Save the Cleaned Data

<!--------------------------------------------------------------------------------------------------------------------------------------------------------------------->

- Data Loading

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }

        .dataframe tbody tr th {
            vertical-align: top;
        }

        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
    <thead>
        <tr style="text-align: right;">
        <th></th>
        <th>institution_name</th>
        <th>main_office</th>
        <th>branch_name</th>
        <th>branch_number</th>
        <th>established_date</th>
        <th>street_address</th>
        <th>city</th>
        <th>county</th>
        <th>state</th>
        <th>zipcode</th>
        <th>latitude</th>
        <th>longitude</th>
        <th>2010_deposits</th>
        <th>2011_deposits</th>
        <th>2012_deposits</th>
        <th>2013_deposits</th>
        <th>2014_deposits</th>
        <th>2015_deposits</th>
        <th>2016_deposits</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <th>0</th>
        <td>JPMorgan Chase Bank</td>
        <td>1</td>
        <td>JPMorgan Chase Bank Main Office</td>
        <td>0</td>
        <td>1824-01-01</td>
        <td>1111 Polaris Parkway</td>
        <td>Columbus</td>
        <td>Delaware</td>
        <td>OH</td>
        <td>43240</td>
        <td>40.14453</td>
        <td>-82.99115</td>
        <td>633131000</td>
        <td>743268000</td>
        <td>832455000</td>
        <td>916543000</td>
        <td>1032549000</td>
        <td>1069425000</td>
        <td>1155185000</td>
        </tr>
        <tr>
        <th>1</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Vernon Hills Scarsdale Branch</td>
        <td>2</td>
        <td>3/20/1961</td>
        <td>676 White Plains Road</td>
        <td>Scarsdale</td>
        <td>Westchester</td>
        <td>NY</td>
        <td>10583</td>
        <td>40.97008</td>
        <td>-73.80670</td>
        <td>293229</td>
        <td>310791</td>
        <td>325742</td>
        <td>327930</td>
        <td>327792</td>
        <td>341475</td>
        <td>381558</td>
        </tr>
        <tr>
        <th>2</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Great Neck Northern Boulevard Branch</td>
        <td>3</td>
        <td>9/9/1963</td>
        <td>410 Northern Boulevard</td>
        <td>Great Neck</td>
        <td>Nassau</td>
        <td>NY</td>
        <td>11021</td>
        <td>40.77944</td>
        <td>-73.72240</td>
        <td>191011</td>
        <td>206933</td>
        <td>216439</td>
        <td>237983</td>
        <td>234183</td>
        <td>262455</td>
        <td>278940</td>
        </tr>
        <tr>
        <th>3</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>North Hartsdale Branch</td>
        <td>4</td>
        <td>2/19/1966</td>
        <td>353 North Central Avenue</td>
        <td>Hartsdale</td>
        <td>Westchester</td>
        <td>NY</td>
        <td>10530</td>
        <td>41.02654</td>
        <td>-73.79168</td>
        <td>87110</td>
        <td>88367</td>
        <td>93163</td>
        <td>109659</td>
        <td>111985</td>
        <td>116772</td>
        <td>140233</td>
        </tr>
        <tr>
        <th>4</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Lawrence Rockaway Branch</td>
        <td>5</td>
        <td>1/16/1965</td>
        <td>335 Rockaway Turnpike</td>
        <td>Lawrence</td>
        <td>Nassau</td>
        <td>NY</td>
        <td>11559</td>
        <td>40.62715</td>
        <td>-73.73675</td>
        <td>172608</td>
        <td>172749</td>
        <td>189413</td>
        <td>198445</td>
        <td>205198</td>
        <td>223200</td>
        <td>235594</td>
        </tr>
        <tr>
        <th>...</th>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        </tr>
        <tr>
        <th>5342</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Alameda and Compton Blvd Branch</td>
        <td>7981</td>
        <td>11/3/2015</td>
        <td>251 E Compton Blvd</td>
        <td>Compton</td>
        <td>Los Angeles</td>
        <td>CA</td>
        <td>90220</td>
        <td>33.89601</td>
        <td>-118.22084</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>3446</td>
        </tr>
        <tr>
        <th>5343</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Charleston and Rancho</td>
        <td>7982</td>
        <td>2/2/2016</td>
        <td>2311 W Chafrleston Blvd</td>
        <td>Las Vegas</td>
        <td>Clark</td>
        <td>NV</td>
        <td>89102</td>
        <td>36.14270</td>
        <td>-115.19043</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>2666</td>
        </tr>
        <tr>
        <th>5344</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Los Olivos Branch</td>
        <td>7984</td>
        <td>3/15/2016</td>
        <td>8593 Irvine Center Drive</td>
        <td>Irvine</td>
        <td>Orange</td>
        <td>CA</td>
        <td>92618</td>
        <td>33.64412</td>
        <td>-117.74453</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>6689</td>
        </tr>
        <tr>
        <th>5345</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Lake Forest Branch</td>
        <td>7988</td>
        <td>1/1/2016</td>
        <td>5660 Read Blvd</td>
        <td>New Orleans</td>
        <td>Orleans</td>
        <td>LA</td>
        <td>70127</td>
        <td>30.03205</td>
        <td>-89.97260</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>94133</td>
        </tr>
        <tr>
        <th>5346</th>
        <td>JPMorgan Chase Bank</td>
        <td>0</td>
        <td>Buffalo-Mm Branch</td>
        <td>7989</td>
        <td>1/1/2016</td>
        <td>350 Main Street</td>
        <td>Buffalo</td>
        <td>Erie</td>
        <td>NY</td>
        <td>14202</td>
        <td>42.88429</td>
        <td>-78.87487</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>45596</td>
        </tr>
    </tbody>
    </table>
    <p>5347 rows × 19 columns</p>
    </div>

<!---------------------------------------------------------------------------------------------------------------------------------------------------------------->

- <h4><a href="/queries/schema.sql">Database Schema Setup</a></h4>

    ```sql
    -- Create Database
    CREATE SCHEMA `chase_bank`;
    ```


<!-------------------------------------------------------------------------------------------------------------------------------------------------------------------->

- <h4><a href="/queries/table.sql">Database Table Setup</a></h4>


    ```sql
    -- Create Table
    CREATE TABLE chase(
        id INT NOT NULL,
        institution_name VARCHAR(255) NOT NULL,
        main_office INT NOT NULL,
        branch_name VARCHAR(255) NOT NULL,
        branch_number INT NOT NULL,
        established_date DATE,
        acquired_date DATE,
        street_address VARCHAR(255),
        city VARCHAR(255),
        county VARCHAR(255),
        state VARCHAR(255),
        zipcode INT,
        latitude DECIMAL(18,9),
        longitude DECIMAL(18,9),
        2011_deposits BIGINT,
        2011_deposits BIGINT,
        2012_deposits BIGINT,
        2013_deposits BIGINT,
        2014_deposits BIGINT,
        2015_deposits BIGINT,
        2016_deposits BIGINT,
        PRIMARY KEY (id)
    );
    ```
<!--------------------------------------------------------------------------------------------------------------------------------------------------------------->

<h2 align="center">Analysis</h2>

<!------------------------------------------------------------------------------------------------------------------------------------------------------------------>

- What are the Top 10 state with the highest deposit amount in 2016?

    ```sql
    SELECT state,SUM(2016_deposits) AS total_deposits_2016
    FROM chase
    GROUP BY state
    ORDER BY total_deposits_2016 DESC;
    ```



    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }

        .dataframe tbody tr th {
            vertical-align: top;
        }

        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
    <thead>
        <tr style="text-align: right;">
        <th></th>
        <th>state</th>
        <th>total_deposits_2016</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <th>0</th>
        <td>NY</td>
        <td>151385380</td>
        </tr>
        <tr>
        <th>1</th>
        <td>TX</td>
        <td>109526094</td>
        </tr>
        <tr>
        <th>2</th>
        <td>CA</td>
        <td>103824272</td>
        </tr>
        <tr>
        <th>3</th>
        <td>IL</td>
        <td>73966280</td>
        </tr>
        <tr>
        <th>4</th>
        <td>MI</td>
        <td>40021790</td>
        </tr>
        <tr>
        <th>5</th>
        <td>AZ</td>
        <td>26181633</td>
        </tr>
        <tr>
        <th>6</th>
        <td>FL</td>
        <td>19710979</td>
        </tr>
        <tr>
        <th>7</th>
        <td>OH</td>
        <td>19068602</td>
        </tr>
        <tr>
        <th>8</th>
        <td>IN</td>
        <td>17070875</td>
        </tr>
        <tr>
        <th>9</th>
        <td>LA</td>
        <td>16989963</td>
        </tr>
        <tr>
        <th>10</th>
        <td>WA</td>
        <td>14659607</td>
        </tr>
        <tr>
        <th>11</th>
        <td>NJ</td>
        <td>13494709</td>
        </tr>
        <tr>
        <th>12</th>
        <td>UT</td>
        <td>11963846</td>
        </tr>
        <tr>
        <th>13</th>
        <td>WI</td>
        <td>9410758</td>
        </tr>
        <tr>
        <th>14</th>
        <td>CO</td>
        <td>8334593</td>
        </tr>
        <tr>
        <th>15</th>
        <td>OR</td>
        <td>5825288</td>
        </tr>
        <tr>
        <th>16</th>
        <td>KY</td>
        <td>5667540</td>
        </tr>
        <tr>
        <th>17</th>
        <td>CT</td>
        <td>4448267</td>
        </tr>
        <tr>
        <th>18</th>
        <td>OK</td>
        <td>2306162</td>
        </tr>
        <tr>
        <th>19</th>
        <td>WV</td>
        <td>1812236</td>
        </tr>
        <tr>
        <th>20</th>
        <td>NV</td>
        <td>1632736</td>
        </tr>
        <tr>
        <th>21</th>
        <td>GA</td>
        <td>1245175</td>
        </tr>
        <tr>
        <th>22</th>
        <td>ID</td>
        <td>653412</td>
        </tr>
        <tr>
        <th>23</th>
        <td>PA</td>
        <td>0</td>
        </tr>
        <tr>
        <th>24</th>
        <td>MA</td>
        <td>0</td>
        </tr>
        <tr>
        <th>25</th>
        <td>DC</td>
        <td>0</td>
        </tr>
    </tbody>
    </table>
    </div>




    ![question1](/assets/question1.png)


---


<!-------------------------------------------------------------------------------------------------------------------------------------------------------->


- What are the Top 5 branches with the highest deposit amount in 2014?


    ```sql
    SELECT branch_name,2014_deposits
    FROM chase
    ORDER BY 2014_deposits DESC
    LIMIT 5;
    ```


    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }

        .dataframe tbody tr th {
            vertical-align: top;
        }

        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
    <thead>
        <tr style="text-align: right;">
        <th></th>
        <th>branch_name</th>
        <th>2014_deposits</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <th>0</th>
        <td>Madison Ave Abd 48th St Branch</td>
        <td>98322162</td>
        </tr>
        <tr>
        <th>1</th>
        <td>Houston Main Office</td>
        <td>82408236</td>
        </tr>
        <tr>
        <th>2</th>
        <td>Chicago's Main Office Branch</td>
        <td>47103774</td>
        </tr>
        <tr>
        <th>3</th>
        <td>Detroit Main Branch</td>
        <td>18121683</td>
        </tr>
        <tr>
        <th>4</th>
        <td>Chase Tower Branch</td>
        <td>5857726</td>
        </tr>
    </tbody>
    </table>
    </div>
    




    ![question2](/assets/question2.png)


---

<!-------------------------------------------------------------------------------------------------------------------------------------------------------->


-   What are the average deposit amount for all branches in each county in 2015?


    ```sql
    SELECT county,AVG(2015_deposits) AS average_deposits_2015
    FROM chase
    GROUP BY county
    ORDER BY average_deposits_2015 DESC;
    ```

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }

        .dataframe tbody tr th {
            vertical-align: top;
        }

        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
    <thead>
        <tr style="text-align: right;">
        <th></th>
        <th>county</th>
        <th>average_deposits_2015</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <th>0</th>
        <td>New York</td>
        <td>1.684863e+06</td>
        </tr>
        <tr>
        <th>1</th>
        <td>Harris</td>
        <td>5.498815e+05</td>
        </tr>
        <tr>
        <th>2</th>
        <td>Cook</td>
        <td>5.017104e+05</td>
        </tr>
        <tr>
        <th>3</th>
        <td>Denver</td>
        <td>4.935599e+05</td>
        </tr>
        <tr>
        <th>4</th>
        <td>Salt Lake</td>
        <td>4.268664e+05</td>
        </tr>
        <tr>
        <th>...</th>
        <td>...</td>
        <td>...</td>
        </tr>
        <tr>
        <th>350</th>
        <td>Box Elder</td>
        <td>1.507100e+04</td>
        </tr>
        <tr>
        <th>351</th>
        <td>Bannock</td>
        <td>1.325100e+04</td>
        </tr>
        <tr>
        <th>352</th>
        <td>Tangipahoa</td>
        <td>1.323900e+04</td>
        </tr>
        <tr>
        <th>353</th>
        <td>Philadelphia</td>
        <td>0.000000e+00</td>
        </tr>
        <tr>
        <th>354</th>
        <td>District of Columbia</td>
        <td>0.000000e+00</td>
        </tr>
    </tbody>
    </table>
    <p>355 rows × 2 columns</p>
    </div>


    ![question3](/assets/question3.png)




---



<!-------------------------------------------------------------------------------------------------------------------------------------------------------->



-   How many branches were established in each year?


    ```sql
    SELECT SUBSTR(established_date,1,4) AS establishment_year,COUNT(*) AS number_of_branches
    FROM chase
    GROUP BY establishment_year
    ORDER BY establishment_year;
    ```




    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }

        .dataframe tbody tr th {
            vertical-align: top;
        }

        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
    <thead>
        <tr style="text-align: right;">
        <th></th>
        <th>establishment_year</th>
        <th>number_of_branches</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <th>0</th>
        <td>1800</td>
        <td>27</td>
        </tr>
        <tr>
        <th>1</th>
        <td>1812</td>
        <td>2</td>
        </tr>
        <tr>
        <th>2</th>
        <td>1814</td>
        <td>2</td>
        </tr>
        <tr>
        <th>3</th>
        <td>1825</td>
        <td>1</td>
        </tr>
        <tr>
        <th>4</th>
        <td>1839</td>
        <td>3</td>
        </tr>
        <tr>
        <th>...</th>
        <td>...</td>
        <td>...</td>
        </tr>
        <tr>
        <th>146</th>
        <td>2004</td>
        <td>136</td>
        </tr>
        <tr>
        <th>147</th>
        <td>2005</td>
        <td>79</td>
        </tr>
        <tr>
        <th>148</th>
        <td>2006</td>
        <td>67</td>
        </tr>
        <tr>
        <th>149</th>
        <td>2007</td>
        <td>51</td>
        </tr>
        <tr>
        <th>150</th>
        <td>2008</td>
        <td>18</td>
        </tr>
    </tbody>
    </table>
    <p>151 rows × 2 columns</p>
    </div>



    ![question4](/assets/question4.png)




---


<!-------------------------------------------------------------------------------------------------------------------------------------------------------->


-   List the top 5 branches with the highest growth in deposits between 2010 and 2016.


    ```sql
    SELECT branch_name,(2016_deposits - 2010_deposits) AS deposit_growth
    FROM chase
    ORDER BY deposit_growth DESC
    LIMIT 5;
    ```


    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }

        .dataframe tbody tr th {
            vertical-align: top;
        }

        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
    <thead>
        <tr style="text-align: right;">
        <th></th>
        <th>branch_name</th>
        <th>deposit_growth</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <th>0</th>
        <td>Houston Main Office</td>
        <td>31464197</td>
        </tr>
        <tr>
        <th>1</th>
        <td>Madison Ave Abd 48th St Branch</td>
        <td>23945710</td>
        </tr>
        <tr>
        <th>2</th>
        <td>Chicago's Main Office Branch</td>
        <td>14437942</td>
        </tr>
        <tr>
        <th>3</th>
        <td>Detroit Main Branch</td>
        <td>12546146</td>
        </tr>
        <tr>
        <th>4</th>
        <td>One Utah Branch</td>
        <td>8415454</td>
        </tr>
    </tbody>
    </table>
    </div>



    ![question5](/assets/question5.png)



---




<!-------------------------------------------------------------------------------------------------------------------------------------------------------->


-   Which branches were established after the year 2000 in Florida?


    ```sql
    SELECT branch_name,established_date
    FROM chase
    WHERE SUBSTR(established_date,1,4) > "2000" AND state = "FL";
    ```




    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }

        .dataframe tbody tr th {
            vertical-align: top;
        }

        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
    <thead>
        <tr style="text-align: right;">
        <th></th>
        <th>branch_name</th>
        <th>established_date</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <th>0</th>
        <td>Aston Gardens Banking Center Branch</td>
        <td>2003-05-23</td>
        </tr>
        <tr>
        <th>1</th>
        <td>Aston Gardens Naples Banking Center Branch</td>
        <td>2004-05-04</td>
        </tr>
        <tr>
        <th>2</th>
        <td>Kendall Park Plaza Branch</td>
        <td>2001-02-05</td>
        </tr>
        <tr>
        <th>3</th>
        <td>Wekiva Branch</td>
        <td>2001-11-13</td>
        </tr>
        <tr>
        <th>4</th>
        <td>Cocoa Commons Branch</td>
        <td>2002-02-04</td>
        </tr>
        <tr>
        <th>...</th>
        <td>...</td>
        <td>...</td>
        </tr>
        <tr>
        <th>76</th>
        <td>West Country Club Branch</td>
        <td>2007-06-25</td>
        </tr>
        <tr>
        <th>77</th>
        <td>Doral Plaza Branch</td>
        <td>2007-07-01</td>
        </tr>
        <tr>
        <th>78</th>
        <td>Mall At 163rd Branch</td>
        <td>2007-08-01</td>
        </tr>
        <tr>
        <th>79</th>
        <td>Stadium Corners Branch</td>
        <td>2007-11-13</td>
        </tr>
        <tr>
        <th>80</th>
        <td>Bay Meadows Branch</td>
        <td>2007-11-13</td>
        </tr>
    </tbody>
    </table>
    <p>81 rows × 2 columns</p>
    </div>


---


<!-------------------------------------------------------------------------------------------------------------------------------------------------------->


-   What are the Top 10 States based on number of branches?


    ```sql
    SELECT state,COUNT(*) AS branch_count
    FROM chase
    GROUP BY state
    ORDER BY branch_count DESC
    LIMIT 10;
    ```




    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }

        .dataframe tbody tr th {
            vertical-align: top;
        }

        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
    <thead>
        <tr style="text-align: right;">
        <th></th>
        <th>state</th>
        <th>branch_count</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <th>0</th>
        <td>CA</td>
        <td>666</td>
        </tr>
        <tr>
        <th>1</th>
        <td>NY</td>
        <td>501</td>
        </tr>
        <tr>
        <th>2</th>
        <td>TX</td>
        <td>444</td>
        </tr>
        <tr>
        <th>3</th>
        <td>OH</td>
        <td>251</td>
        </tr>
        <tr>
        <th>4</th>
        <td>IL</td>
        <td>219</td>
        </tr>
        <tr>
        <th>5</th>
        <td>MI</td>
        <td>217</td>
        </tr>
        <tr>
        <th>6</th>
        <td>FL</td>
        <td>207</td>
        </tr>
        <tr>
        <th>7</th>
        <td>WA</td>
        <td>182</td>
        </tr>
        <tr>
        <th>8</th>
        <td>AZ</td>
        <td>171</td>
        </tr>
        <tr>
        <th>9</th>
        <td>IN</td>
        <td>162</td>
        </tr>
    </tbody>
    </table>
    </div>



    ![question7](/assets/question7.png)



---


<!-------------------------------------------------------------------------------------------------------------------------------------------------------->


-   What is the total number of branches where the branch_name contains the word 'Bank'?


    ```sql
    SELECT COUNT(*) AS total_branches
    FROM chase
    WHERE branch_name LIKE "%Bank%";
    ```


    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }

        .dataframe tbody tr th {
            vertical-align: top;
        }

        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
    <thead>
        <tr style="text-align: right;">
        <!--<th>S/N</th>-->
        <th>total_branches</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <!--<th></th>-->
        <td>165</td>
        </tr>
    </tbody>
    </table>
    </div>




---

<!-------------------------------------------------------------------------------------------------------------------------------------------------------->

- what are the difference in deposits between 2016 and 2010 for branches in each city?



    ```sql
    SELECT city,SUM(2016_deposits) - SUM(2010_deposits) AS deposit_difference
    FROM chase
    GROUP BY city
    ORDER BY deposit_difference DESC;
    ```

    <div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }

        .dataframe tbody tr th {
            vertical-align: top;
        }

        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
    <thead>
        <tr style="text-align: right;">
        <th></th>
        <th>city</th>
        <th>deposit_difference</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <th>0</th>
        <td>Houston</td>
        <td>37149291</td>
        </tr>
        <tr>
        <th>1</th>
        <td>New York City</td>
        <td>31687570</td>
        </tr>
        <tr>
        <th>2</th>
        <td>Chicago</td>
        <td>17992604</td>
        </tr>
        <tr>
        <th>3</th>
        <td>Detroit</td>
        <td>12724043</td>
        </tr>
        <tr>
        <th>4</th>
        <td>Salt Lake City</td>
        <td>8824071</td>
        </tr>
        <tr>
        <th>...</th>
        <td>...</td>
        <td>...</td>
        </tr>
        <tr>
        <th>1548</th>
        <td>Wichita Falls</td>
        <td>-44603</td>
        </tr>
        <tr>
        <th>1549</th>
        <td>Merrillville</td>
        <td>-46079</td>
        </tr>
        <tr>
        <th>1550</th>
        <td>Amarillo</td>
        <td>-48956</td>
        </tr>
        <tr>
        <th>1551</th>
        <td>Elk Grove Village</td>
        <td>-68374</td>
        </tr>
        <tr>
        <th>1552</th>
        <td>Park City</td>
        <td>-3505400</td>
        </tr>
    </tbody>
    </table>
    <p>1553 rows × 2 columns</p>
    </div>