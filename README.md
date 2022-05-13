{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# The World Happiness Report Data Analysis"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Table of Contents\n",
    "\n",
    "\n",
    "[A. Importing, cleaning and numerical summaries](#Import) <br>\n",
    "[B. Indexing and grouping](#Indexing) <br>\n",
    "[C. Bar plot of the Happiness Score](#plot) <br>\n",
    "[D. Histogram of Job Satisfaction](#hist) <br>\n",
    "[E. Pairwise Scatter plots](#scat) <br>\n",
    "[F. Correlation](#corr) <br>\n",
    "[G. Probabilities](#prob) <br>\n",
    "[H. Matrices](#mat)\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "***"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## A. Importing, cleaning and numerical summaries\n",
    "<a id=\"Import\" > "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "1. Download the data set data.csv from the Resources tab.\n",
    "2. Import the data as a pandas DataFrame.\n",
    "3. Check the number of observations.\n",
    "4. Obtain the column headings.\n",
    "5. Check the data type for each column.\n",
    "6. Check if there are any missing values.\n",
    "7. If necessary remove any observations to ensure that there are no missing values and the values in each column are of the same data type.\n",
    "8. Obtain the mean, minimum and maximum value for each column containing numerical data.\n",
    "9. List the 10 happiest countries.\n",
    "10. List the 10 least happy countries."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "import numpy as np\n",
    "import matplotlib.pyplot as plt\n",
    "import seaborn as sns\n",
    "%matplotlib inline"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "WHR = pd.read_csv(\"data.csv\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 382,
   "metadata": {
    "scrolled": False
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Country</th>\n",
       "      <th>Happiness Rank</th>\n",
       "      <th>Happiness Score</th>\n",
       "      <th>Economy</th>\n",
       "      <th>Family</th>\n",
       "      <th>Health</th>\n",
       "      <th>Freedom</th>\n",
       "      <th>Generosity</th>\n",
       "      <th>Corruption</th>\n",
       "      <th>Dystopia</th>\n",
       "      <th>Job Satisfaction</th>\n",
       "      <th>Region</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Norway</td>\n",
       "      <td>1</td>\n",
       "      <td>7.537</td>\n",
       "      <td>1.616463</td>\n",
       "      <td>1.533524</td>\n",
       "      <td>0.796667</td>\n",
       "      <td>0.635423</td>\n",
       "      <td>0.362012</td>\n",
       "      <td>0.315964</td>\n",
       "      <td>2.277027</td>\n",
       "      <td>94.6</td>\n",
       "      <td>Western Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Denmark</td>\n",
       "      <td>2</td>\n",
       "      <td>7.522</td>\n",
       "      <td>1.482383</td>\n",
       "      <td>1.551122</td>\n",
       "      <td>0.792566</td>\n",
       "      <td>0.626007</td>\n",
       "      <td>0.355280</td>\n",
       "      <td>0.400770</td>\n",
       "      <td>2.313707</td>\n",
       "      <td>93.5</td>\n",
       "      <td>Western Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Iceland</td>\n",
       "      <td>3</td>\n",
       "      <td>7.504</td>\n",
       "      <td>1.480633</td>\n",
       "      <td>1.610574</td>\n",
       "      <td>0.833552</td>\n",
       "      <td>0.627163</td>\n",
       "      <td>0.475540</td>\n",
       "      <td>0.153527</td>\n",
       "      <td>2.322715</td>\n",
       "      <td>94.5</td>\n",
       "      <td>Western Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Switzerland</td>\n",
       "      <td>4</td>\n",
       "      <td>7.494</td>\n",
       "      <td>1.564980</td>\n",
       "      <td>1.516912</td>\n",
       "      <td>0.858131</td>\n",
       "      <td>0.620071</td>\n",
       "      <td>0.290549</td>\n",
       "      <td>0.367007</td>\n",
       "      <td>2.276716</td>\n",
       "      <td>93.7</td>\n",
       "      <td>Western Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Finland</td>\n",
       "      <td>5</td>\n",
       "      <td>7.469</td>\n",
       "      <td>1.443572</td>\n",
       "      <td>1.540247</td>\n",
       "      <td>0.809158</td>\n",
       "      <td>0.617951</td>\n",
       "      <td>0.245483</td>\n",
       "      <td>0.382612</td>\n",
       "      <td>2.430182</td>\n",
       "      <td>91.2</td>\n",
       "      <td>Western Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>Netherlands</td>\n",
       "      <td>6</td>\n",
       "      <td>7.377</td>\n",
       "      <td>1.503945</td>\n",
       "      <td>1.428939</td>\n",
       "      <td>0.810696</td>\n",
       "      <td>0.585384</td>\n",
       "      <td>0.470490</td>\n",
       "      <td>0.282662</td>\n",
       "      <td>2.294804</td>\n",
       "      <td>93.8</td>\n",
       "      <td>Western Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>Canada</td>\n",
       "      <td>7</td>\n",
       "      <td>7.316</td>\n",
       "      <td>1.479204</td>\n",
       "      <td>1.481349</td>\n",
       "      <td>0.834558</td>\n",
       "      <td>0.611101</td>\n",
       "      <td>0.435540</td>\n",
       "      <td>0.287372</td>\n",
       "      <td>2.187264</td>\n",
       "      <td>90.5</td>\n",
       "      <td>North America</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>New Zealand</td>\n",
       "      <td>8</td>\n",
       "      <td>7.314</td>\n",
       "      <td>1.405706</td>\n",
       "      <td>1.548195</td>\n",
       "      <td>0.816760</td>\n",
       "      <td>0.614062</td>\n",
       "      <td>0.500005</td>\n",
       "      <td>0.382817</td>\n",
       "      <td>2.046456</td>\n",
       "      <td>88.6</td>\n",
       "      <td>Asia-Pacific</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8</th>\n",
       "      <td>Sweden</td>\n",
       "      <td>9</td>\n",
       "      <td>7.284</td>\n",
       "      <td>1.494387</td>\n",
       "      <td>1.478162</td>\n",
       "      <td>0.830875</td>\n",
       "      <td>0.612924</td>\n",
       "      <td>0.385399</td>\n",
       "      <td>0.384399</td>\n",
       "      <td>2.097538</td>\n",
       "      <td>92.7</td>\n",
       "      <td>Western Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>9</th>\n",
       "      <td>Australia</td>\n",
       "      <td>10</td>\n",
       "      <td>7.284</td>\n",
       "      <td>1.484415</td>\n",
       "      <td>1.510042</td>\n",
       "      <td>0.843887</td>\n",
       "      <td>0.601607</td>\n",
       "      <td>0.477699</td>\n",
       "      <td>0.301184</td>\n",
       "      <td>2.065211</td>\n",
       "      <td>89.2</td>\n",
       "      <td>Asia-Pacific</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "       Country  Happiness Rank  Happiness Score   Economy    Family    Health  \\\n",
       "0       Norway               1            7.537  1.616463  1.533524  0.796667   \n",
       "1      Denmark               2            7.522  1.482383  1.551122  0.792566   \n",
       "2      Iceland               3            7.504  1.480633  1.610574  0.833552   \n",
       "3  Switzerland               4            7.494  1.564980  1.516912  0.858131   \n",
       "4      Finland               5            7.469  1.443572  1.540247  0.809158   \n",
       "5  Netherlands               6            7.377  1.503945  1.428939  0.810696   \n",
       "6       Canada               7            7.316  1.479204  1.481349  0.834558   \n",
       "7  New Zealand               8            7.314  1.405706  1.548195  0.816760   \n",
       "8       Sweden               9            7.284  1.494387  1.478162  0.830875   \n",
       "9    Australia              10            7.284  1.484415  1.510042  0.843887   \n",
       "\n",
       "    Freedom  Generosity  Corruption  Dystopia  Job Satisfaction  \\\n",
       "0  0.635423    0.362012    0.315964  2.277027              94.6   \n",
       "1  0.626007    0.355280    0.400770  2.313707              93.5   \n",
       "2  0.627163    0.475540    0.153527  2.322715              94.5   \n",
       "3  0.620071    0.290549    0.367007  2.276716              93.7   \n",
       "4  0.617951    0.245483    0.382612  2.430182              91.2   \n",
       "5  0.585384    0.470490    0.282662  2.294804              93.8   \n",
       "6  0.611101    0.435540    0.287372  2.187264              90.5   \n",
       "7  0.614062    0.500005    0.382817  2.046456              88.6   \n",
       "8  0.612924    0.385399    0.384399  2.097538              92.7   \n",
       "9  0.601607    0.477699    0.301184  2.065211              89.2   \n",
       "\n",
       "           Region  \n",
       "0  Western Europe  \n",
       "1  Western Europe  \n",
       "2  Western Europe  \n",
       "3  Western Europe  \n",
       "4  Western Europe  \n",
       "5  Western Europe  \n",
       "6   North America  \n",
       "7    Asia-Pacific  \n",
       "8  Western Europe  \n",
       "9    Asia-Pacific  "
      ]
     },
     "execution_count": 382,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR.head(10)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 391,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(151, 11)"
      ]
     },
     "execution_count": 391,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "There are 153 rows and 12 columns in our data\n"
     ]
    }
   ],
   "source": [
    "print(\"There are {:,} rows \".format(WHR.shape[0]) + \"and {} columns in our data\".format(WHR.shape[1]))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 384,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "WHR.set_index('Country', inplace=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 385,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "Index: 153 entries, Norway to Central African Republic\n",
      "Data columns (total 11 columns):\n",
      "Happiness Rank      153 non-null int64\n",
      "Happiness Score     153 non-null float64\n",
      "Economy             153 non-null float64\n",
      "Family              153 non-null float64\n",
      "Health              153 non-null float64\n",
      "Freedom             153 non-null float64\n",
      "Generosity          153 non-null float64\n",
      "Corruption          153 non-null float64\n",
      "Dystopia            153 non-null float64\n",
      "Job Satisfaction    151 non-null float64\n",
      "Region              153 non-null object\n",
      "dtypes: float64(9), int64(1), object(1)\n",
      "memory usage: 14.3+ KB\n"
     ]
    }
   ],
   "source": [
    "WHR.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Country             0\n",
       "Happiness Rank      0\n",
       "Happiness Score     0\n",
       "Economy             0\n",
       "Family              0\n",
       "Health              0\n",
       "Freedom             0\n",
       "Generosity          0\n",
       "Corruption          0\n",
       "Dystopia            0\n",
       "Job Satisfaction    2\n",
       "Region              0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR.isnull().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 387,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "NULLS = WHR[WHR.isnull().any(axis=1)]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 388,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Happiness Rank</th>\n",
       "      <th>Happiness Score</th>\n",
       "      <th>Economy</th>\n",
       "      <th>Family</th>\n",
       "      <th>Health</th>\n",
       "      <th>Freedom</th>\n",
       "      <th>Generosity</th>\n",
       "      <th>Corruption</th>\n",
       "      <th>Dystopia</th>\n",
       "      <th>Job Satisfaction</th>\n",
       "      <th>Region</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Country</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>North Cyprus</th>\n",
       "      <td>61</td>\n",
       "      <td>5.810</td>\n",
       "      <td>1.346911</td>\n",
       "      <td>1.186303</td>\n",
       "      <td>0.834647</td>\n",
       "      <td>0.471204</td>\n",
       "      <td>0.266846</td>\n",
       "      <td>0.155353</td>\n",
       "      <td>1.549158</td>\n",
       "      <td>NaN</td>\n",
       "      <td>Eastern Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>South Sudan</th>\n",
       "      <td>147</td>\n",
       "      <td>3.591</td>\n",
       "      <td>0.397249</td>\n",
       "      <td>0.601323</td>\n",
       "      <td>0.163486</td>\n",
       "      <td>0.147062</td>\n",
       "      <td>0.285671</td>\n",
       "      <td>0.116794</td>\n",
       "      <td>1.879567</td>\n",
       "      <td>NaN</td>\n",
       "      <td>Africa</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "              Happiness Rank  Happiness Score   Economy    Family    Health  \\\n",
       "Country                                                                       \n",
       "North Cyprus              61            5.810  1.346911  1.186303  0.834647   \n",
       "South Sudan              147            3.591  0.397249  0.601323  0.163486   \n",
       "\n",
       "               Freedom  Generosity  Corruption  Dystopia  Job Satisfaction  \\\n",
       "Country                                                                      \n",
       "North Cyprus  0.471204    0.266846    0.155353  1.549158               NaN   \n",
       "South Sudan   0.147062    0.285671    0.116794  1.879567               NaN   \n",
       "\n",
       "                      Region  \n",
       "Country                       \n",
       "North Cyprus  Eastern Europe  \n",
       "South Sudan           Africa  "
      ]
     },
     "execution_count": 388,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "NULLS.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 389,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "WHR.dropna(inplace=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Country             0\n",
       "Happiness Rank      0\n",
       "Happiness Score     0\n",
       "Economy             0\n",
       "Family              0\n",
       "Health              0\n",
       "Freedom             0\n",
       "Generosity          0\n",
       "Corruption          0\n",
       "Dystopia            0\n",
       "Job Satisfaction    0\n",
       "Region              0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 22,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR.isnull().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 392,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0"
      ]
     },
     "execution_count": 392,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR.duplicated().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 395,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Happiness Rank</th>\n",
       "      <th>Happiness Score</th>\n",
       "      <th>Economy</th>\n",
       "      <th>Family</th>\n",
       "      <th>Health</th>\n",
       "      <th>Freedom</th>\n",
       "      <th>Generosity</th>\n",
       "      <th>Corruption</th>\n",
       "      <th>Dystopia</th>\n",
       "      <th>Job Satisfaction</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>151.000000</td>\n",
       "      <td>151.000000</td>\n",
       "      <td>151.000000</td>\n",
       "      <td>151.000000</td>\n",
       "      <td>151.000000</td>\n",
       "      <td>151.000000</td>\n",
       "      <td>151.000000</td>\n",
       "      <td>151.000000</td>\n",
       "      <td>151.000000</td>\n",
       "      <td>151.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>77.827815</td>\n",
       "      <td>5.357874</td>\n",
       "      <td>0.983895</td>\n",
       "      <td>1.190509</td>\n",
       "      <td>0.550794</td>\n",
       "      <td>0.409805</td>\n",
       "      <td>0.244914</td>\n",
       "      <td>0.123008</td>\n",
       "      <td>1.854910</td>\n",
       "      <td>75.209934</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>44.934732</td>\n",
       "      <td>1.132826</td>\n",
       "      <td>0.420955</td>\n",
       "      <td>0.286371</td>\n",
       "      <td>0.236116</td>\n",
       "      <td>0.150144</td>\n",
       "      <td>0.135236</td>\n",
       "      <td>0.102776</td>\n",
       "      <td>0.502189</td>\n",
       "      <td>12.962365</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1.000000</td>\n",
       "      <td>2.693000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.377914</td>\n",
       "      <td>44.400000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>39.500000</td>\n",
       "      <td>4.505500</td>\n",
       "      <td>0.663371</td>\n",
       "      <td>1.042635</td>\n",
       "      <td>0.369866</td>\n",
       "      <td>0.303677</td>\n",
       "      <td>0.152574</td>\n",
       "      <td>0.056919</td>\n",
       "      <td>1.605148</td>\n",
       "      <td>68.950000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>78.000000</td>\n",
       "      <td>5.279000</td>\n",
       "      <td>1.064578</td>\n",
       "      <td>1.253918</td>\n",
       "      <td>0.606042</td>\n",
       "      <td>0.437454</td>\n",
       "      <td>0.230947</td>\n",
       "      <td>0.089283</td>\n",
       "      <td>1.832910</td>\n",
       "      <td>78.100000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>116.500000</td>\n",
       "      <td>6.101500</td>\n",
       "      <td>1.314879</td>\n",
       "      <td>1.418162</td>\n",
       "      <td>0.715975</td>\n",
       "      <td>0.519467</td>\n",
       "      <td>0.323762</td>\n",
       "      <td>0.152207</td>\n",
       "      <td>2.161605</td>\n",
       "      <td>85.100000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>155.000000</td>\n",
       "      <td>7.537000</td>\n",
       "      <td>1.870766</td>\n",
       "      <td>1.610574</td>\n",
       "      <td>0.949492</td>\n",
       "      <td>0.658249</td>\n",
       "      <td>0.838075</td>\n",
       "      <td>0.464308</td>\n",
       "      <td>3.117485</td>\n",
       "      <td>95.100000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "       Happiness Rank  Happiness Score     Economy      Family      Health  \\\n",
       "count      151.000000       151.000000  151.000000  151.000000  151.000000   \n",
       "mean        77.827815         5.357874    0.983895    1.190509    0.550794   \n",
       "std         44.934732         1.132826    0.420955    0.286371    0.236116   \n",
       "min          1.000000         2.693000    0.000000    0.000000    0.000000   \n",
       "25%         39.500000         4.505500    0.663371    1.042635    0.369866   \n",
       "50%         78.000000         5.279000    1.064578    1.253918    0.606042   \n",
       "75%        116.500000         6.101500    1.314879    1.418162    0.715975   \n",
       "max        155.000000         7.537000    1.870766    1.610574    0.949492   \n",
       "\n",
       "          Freedom  Generosity  Corruption    Dystopia  Job Satisfaction  \n",
       "count  151.000000  151.000000  151.000000  151.000000        151.000000  \n",
       "mean     0.409805    0.244914    0.123008    1.854910         75.209934  \n",
       "std      0.150144    0.135236    0.102776    0.502189         12.962365  \n",
       "min      0.000000    0.000000    0.000000    0.377914         44.400000  \n",
       "25%      0.303677    0.152574    0.056919    1.605148         68.950000  \n",
       "50%      0.437454    0.230947    0.089283    1.832910         78.100000  \n",
       "75%      0.519467    0.323762    0.152207    2.161605         85.100000  \n",
       "max      0.658249    0.838075    0.464308    3.117485         95.100000  "
      ]
     },
     "execution_count": 395,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR.describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 394,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Happiness Rank</th>\n",
       "      <th>Happiness Score</th>\n",
       "      <th>Economy</th>\n",
       "      <th>Family</th>\n",
       "      <th>Health</th>\n",
       "      <th>Freedom</th>\n",
       "      <th>Generosity</th>\n",
       "      <th>Corruption</th>\n",
       "      <th>Dystopia</th>\n",
       "      <th>Job Satisfaction</th>\n",
       "      <th>Region</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Country</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>Norway</th>\n",
       "      <td>1</td>\n",
       "      <td>7.537</td>\n",
       "      <td>1.616463</td>\n",
       "      <td>1.533524</td>\n",
       "      <td>0.796667</td>\n",
       "      <td>0.635423</td>\n",
       "      <td>0.362012</td>\n",
       "      <td>0.315964</td>\n",
       "      <td>2.277027</td>\n",
       "      <td>94.6</td>\n",
       "      <td>Western Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Denmark</th>\n",
       "      <td>2</td>\n",
       "      <td>7.522</td>\n",
       "      <td>1.482383</td>\n",
       "      <td>1.551122</td>\n",
       "      <td>0.792566</td>\n",
       "      <td>0.626007</td>\n",
       "      <td>0.355280</td>\n",
       "      <td>0.400770</td>\n",
       "      <td>2.313707</td>\n",
       "      <td>93.5</td>\n",
       "      <td>Western Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Iceland</th>\n",
       "      <td>3</td>\n",
       "      <td>7.504</td>\n",
       "      <td>1.480633</td>\n",
       "      <td>1.610574</td>\n",
       "      <td>0.833552</td>\n",
       "      <td>0.627163</td>\n",
       "      <td>0.475540</td>\n",
       "      <td>0.153527</td>\n",
       "      <td>2.322715</td>\n",
       "      <td>94.5</td>\n",
       "      <td>Western Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Switzerland</th>\n",
       "      <td>4</td>\n",
       "      <td>7.494</td>\n",
       "      <td>1.564980</td>\n",
       "      <td>1.516912</td>\n",
       "      <td>0.858131</td>\n",
       "      <td>0.620071</td>\n",
       "      <td>0.290549</td>\n",
       "      <td>0.367007</td>\n",
       "      <td>2.276716</td>\n",
       "      <td>93.7</td>\n",
       "      <td>Western Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Finland</th>\n",
       "      <td>5</td>\n",
       "      <td>7.469</td>\n",
       "      <td>1.443572</td>\n",
       "      <td>1.540247</td>\n",
       "      <td>0.809158</td>\n",
       "      <td>0.617951</td>\n",
       "      <td>0.245483</td>\n",
       "      <td>0.382612</td>\n",
       "      <td>2.430182</td>\n",
       "      <td>91.2</td>\n",
       "      <td>Western Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Netherlands</th>\n",
       "      <td>6</td>\n",
       "      <td>7.377</td>\n",
       "      <td>1.503945</td>\n",
       "      <td>1.428939</td>\n",
       "      <td>0.810696</td>\n",
       "      <td>0.585384</td>\n",
       "      <td>0.470490</td>\n",
       "      <td>0.282662</td>\n",
       "      <td>2.294804</td>\n",
       "      <td>93.8</td>\n",
       "      <td>Western Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Canada</th>\n",
       "      <td>7</td>\n",
       "      <td>7.316</td>\n",
       "      <td>1.479204</td>\n",
       "      <td>1.481349</td>\n",
       "      <td>0.834558</td>\n",
       "      <td>0.611101</td>\n",
       "      <td>0.435540</td>\n",
       "      <td>0.287372</td>\n",
       "      <td>2.187264</td>\n",
       "      <td>90.5</td>\n",
       "      <td>North America</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>New Zealand</th>\n",
       "      <td>8</td>\n",
       "      <td>7.314</td>\n",
       "      <td>1.405706</td>\n",
       "      <td>1.548195</td>\n",
       "      <td>0.816760</td>\n",
       "      <td>0.614062</td>\n",
       "      <td>0.500005</td>\n",
       "      <td>0.382817</td>\n",
       "      <td>2.046456</td>\n",
       "      <td>88.6</td>\n",
       "      <td>Asia-Pacific</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Sweden</th>\n",
       "      <td>9</td>\n",
       "      <td>7.284</td>\n",
       "      <td>1.494387</td>\n",
       "      <td>1.478162</td>\n",
       "      <td>0.830875</td>\n",
       "      <td>0.612924</td>\n",
       "      <td>0.385399</td>\n",
       "      <td>0.384399</td>\n",
       "      <td>2.097538</td>\n",
       "      <td>92.7</td>\n",
       "      <td>Western Europe</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Australia</th>\n",
       "      <td>10</td>\n",
       "      <td>7.284</td>\n",
       "      <td>1.484415</td>\n",
       "      <td>1.510042</td>\n",
       "      <td>0.843887</td>\n",
       "      <td>0.601607</td>\n",
       "      <td>0.477699</td>\n",
       "      <td>0.301184</td>\n",
       "      <td>2.065211</td>\n",
       "      <td>89.2</td>\n",
       "      <td>Asia-Pacific</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "             Happiness Rank  Happiness Score   Economy    Family    Health  \\\n",
       "Country                                                                      \n",
       "Norway                    1            7.537  1.616463  1.533524  0.796667   \n",
       "Denmark                   2            7.522  1.482383  1.551122  0.792566   \n",
       "Iceland                   3            7.504  1.480633  1.610574  0.833552   \n",
       "Switzerland               4            7.494  1.564980  1.516912  0.858131   \n",
       "Finland                   5            7.469  1.443572  1.540247  0.809158   \n",
       "Netherlands               6            7.377  1.503945  1.428939  0.810696   \n",
       "Canada                    7            7.316  1.479204  1.481349  0.834558   \n",
       "New Zealand               8            7.314  1.405706  1.548195  0.816760   \n",
       "Sweden                    9            7.284  1.494387  1.478162  0.830875   \n",
       "Australia                10            7.284  1.484415  1.510042  0.843887   \n",
       "\n",
       "              Freedom  Generosity  Corruption  Dystopia  Job Satisfaction  \\\n",
       "Country                                                                     \n",
       "Norway       0.635423    0.362012    0.315964  2.277027              94.6   \n",
       "Denmark      0.626007    0.355280    0.400770  2.313707              93.5   \n",
       "Iceland      0.627163    0.475540    0.153527  2.322715              94.5   \n",
       "Switzerland  0.620071    0.290549    0.367007  2.276716              93.7   \n",
       "Finland      0.617951    0.245483    0.382612  2.430182              91.2   \n",
       "Netherlands  0.585384    0.470490    0.282662  2.294804              93.8   \n",
       "Canada       0.611101    0.435540    0.287372  2.187264              90.5   \n",
       "New Zealand  0.614062    0.500005    0.382817  2.046456              88.6   \n",
       "Sweden       0.612924    0.385399    0.384399  2.097538              92.7   \n",
       "Australia    0.601607    0.477699    0.301184  2.065211              89.2   \n",
       "\n",
       "                     Region  \n",
       "Country                      \n",
       "Norway       Western Europe  \n",
       "Denmark      Western Europe  \n",
       "Iceland      Western Europe  \n",
       "Switzerland  Western Europe  \n",
       "Finland      Western Europe  \n",
       "Netherlands  Western Europe  \n",
       "Canada        North America  \n",
       "New Zealand    Asia-Pacific  \n",
       "Sweden       Western Europe  \n",
       "Australia      Asia-Pacific  "
      ]
     },
     "execution_count": 394,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR.sort_values(by=\"Happiness Rank\", ascending=True).head(10)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 396,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Happiness Rank</th>\n",
       "      <th>Happiness Score</th>\n",
       "      <th>Economy</th>\n",
       "      <th>Family</th>\n",
       "      <th>Health</th>\n",
       "      <th>Freedom</th>\n",
       "      <th>Generosity</th>\n",
       "      <th>Corruption</th>\n",
       "      <th>Dystopia</th>\n",
       "      <th>Job Satisfaction</th>\n",
       "      <th>Region</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Country</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>Central African Republic</th>\n",
       "      <td>155</td>\n",
       "      <td>2.693</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.018773</td>\n",
       "      <td>0.270842</td>\n",
       "      <td>0.280876</td>\n",
       "      <td>0.056565</td>\n",
       "      <td>2.066005</td>\n",
       "      <td>70.4</td>\n",
       "      <td>Africa</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Burundi</th>\n",
       "      <td>154</td>\n",
       "      <td>2.905</td>\n",
       "      <td>0.091623</td>\n",
       "      <td>0.629794</td>\n",
       "      <td>0.151611</td>\n",
       "      <td>0.059901</td>\n",
       "      <td>0.204435</td>\n",
       "      <td>0.084148</td>\n",
       "      <td>1.683024</td>\n",
       "      <td>54.3</td>\n",
       "      <td>Africa</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Tanzania</th>\n",
       "      <td>153</td>\n",
       "      <td>3.349</td>\n",
       "      <td>0.511136</td>\n",
       "      <td>1.041990</td>\n",
       "      <td>0.364509</td>\n",
       "      <td>0.390018</td>\n",
       "      <td>0.354256</td>\n",
       "      <td>0.066035</td>\n",
       "      <td>0.621130</td>\n",
       "      <td>57.8</td>\n",
       "      <td>Africa</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Syria</th>\n",
       "      <td>152</td>\n",
       "      <td>3.462</td>\n",
       "      <td>0.777153</td>\n",
       "      <td>0.396103</td>\n",
       "      <td>0.500533</td>\n",
       "      <td>0.081539</td>\n",
       "      <td>0.493664</td>\n",
       "      <td>0.151347</td>\n",
       "      <td>1.061574</td>\n",
       "      <td>62.7</td>\n",
       "      <td>Asia-Pacific</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Rwanda</th>\n",
       "      <td>151</td>\n",
       "      <td>3.471</td>\n",
       "      <td>0.368746</td>\n",
       "      <td>0.945707</td>\n",
       "      <td>0.326425</td>\n",
       "      <td>0.581844</td>\n",
       "      <td>0.252756</td>\n",
       "      <td>0.455220</td>\n",
       "      <td>0.540061</td>\n",
       "      <td>51.7</td>\n",
       "      <td>Africa</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Togo</th>\n",
       "      <td>150</td>\n",
       "      <td>3.495</td>\n",
       "      <td>0.305445</td>\n",
       "      <td>0.431883</td>\n",
       "      <td>0.247106</td>\n",
       "      <td>0.380426</td>\n",
       "      <td>0.196896</td>\n",
       "      <td>0.095665</td>\n",
       "      <td>1.837229</td>\n",
       "      <td>44.8</td>\n",
       "      <td>Africa</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Guinea</th>\n",
       "      <td>149</td>\n",
       "      <td>3.507</td>\n",
       "      <td>0.244550</td>\n",
       "      <td>0.791245</td>\n",
       "      <td>0.194129</td>\n",
       "      <td>0.348588</td>\n",
       "      <td>0.264815</td>\n",
       "      <td>0.110938</td>\n",
       "      <td>1.552312</td>\n",
       "      <td>55.1</td>\n",
       "      <td>Africa</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Liberia</th>\n",
       "      <td>148</td>\n",
       "      <td>3.533</td>\n",
       "      <td>0.119042</td>\n",
       "      <td>0.872118</td>\n",
       "      <td>0.229918</td>\n",
       "      <td>0.332881</td>\n",
       "      <td>0.266550</td>\n",
       "      <td>0.038948</td>\n",
       "      <td>1.673286</td>\n",
       "      <td>56.6</td>\n",
       "      <td>Africa</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Yemen</th>\n",
       "      <td>146</td>\n",
       "      <td>3.593</td>\n",
       "      <td>0.591683</td>\n",
       "      <td>0.935382</td>\n",
       "      <td>0.310081</td>\n",
       "      <td>0.249464</td>\n",
       "      <td>0.104125</td>\n",
       "      <td>0.056767</td>\n",
       "      <td>1.345601</td>\n",
       "      <td>58.9</td>\n",
       "      <td>Asia-Pacific</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Haiti</th>\n",
       "      <td>145</td>\n",
       "      <td>3.603</td>\n",
       "      <td>0.368610</td>\n",
       "      <td>0.640450</td>\n",
       "      <td>0.277321</td>\n",
       "      <td>0.030370</td>\n",
       "      <td>0.489204</td>\n",
       "      <td>0.099872</td>\n",
       "      <td>1.697168</td>\n",
       "      <td>48.5</td>\n",
       "      <td>Latin America</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                          Happiness Rank  Happiness Score   Economy    Family  \\\n",
       "Country                                                                         \n",
       "Central African Republic             155            2.693  0.000000  0.000000   \n",
       "Burundi                              154            2.905  0.091623  0.629794   \n",
       "Tanzania                             153            3.349  0.511136  1.041990   \n",
       "Syria                                152            3.462  0.777153  0.396103   \n",
       "Rwanda                               151            3.471  0.368746  0.945707   \n",
       "Togo                                 150            3.495  0.305445  0.431883   \n",
       "Guinea                               149            3.507  0.244550  0.791245   \n",
       "Liberia                              148            3.533  0.119042  0.872118   \n",
       "Yemen                                146            3.593  0.591683  0.935382   \n",
       "Haiti                                145            3.603  0.368610  0.640450   \n",
       "\n",
       "                            Health   Freedom  Generosity  Corruption  \\\n",
       "Country                                                                \n",
       "Central African Republic  0.018773  0.270842    0.280876    0.056565   \n",
       "Burundi                   0.151611  0.059901    0.204435    0.084148   \n",
       "Tanzania                  0.364509  0.390018    0.354256    0.066035   \n",
       "Syria                     0.500533  0.081539    0.493664    0.151347   \n",
       "Rwanda                    0.326425  0.581844    0.252756    0.455220   \n",
       "Togo                      0.247106  0.380426    0.196896    0.095665   \n",
       "Guinea                    0.194129  0.348588    0.264815    0.110938   \n",
       "Liberia                   0.229918  0.332881    0.266550    0.038948   \n",
       "Yemen                     0.310081  0.249464    0.104125    0.056767   \n",
       "Haiti                     0.277321  0.030370    0.489204    0.099872   \n",
       "\n",
       "                          Dystopia  Job Satisfaction         Region  \n",
       "Country                                                              \n",
       "Central African Republic  2.066005              70.4         Africa  \n",
       "Burundi                   1.683024              54.3         Africa  \n",
       "Tanzania                  0.621130              57.8         Africa  \n",
       "Syria                     1.061574              62.7   Asia-Pacific  \n",
       "Rwanda                    0.540061              51.7         Africa  \n",
       "Togo                      1.837229              44.8         Africa  \n",
       "Guinea                    1.552312              55.1         Africa  \n",
       "Liberia                   1.673286              56.6         Africa  \n",
       "Yemen                     1.345601              58.9   Asia-Pacific  \n",
       "Haiti                     1.697168              48.5  Latin America  "
      ]
     },
     "execution_count": 396,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR.sort_values(by=\"Happiness Rank\", ascending=False).head(10)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "***"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## B. Indexing and grouping\n",
    "<a id=\"Indexing\" > "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "1. Use the column 'Region' to create a separate DataFrame containing the data points from each of the six regions: North America, Latin America, Western Europe, Eastern Europe, Asia Pacific, Africa.\n",
    "2. Compute the mean happiness score for each region and rank the regions from most happy to least happy.\n",
    "3. Compute the number of countries in each region that have a happiness score above 6.0.\n",
    "4. Compute the difference between the maximum and minimum happiness score for each region. Which region has the largest range of happiness scores?"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 397,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "WHR_Region = WHR.groupby('Region')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 398,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>count</th>\n",
       "      <th>mean</th>\n",
       "      <th>std</th>\n",
       "      <th>min</th>\n",
       "      <th>25%</th>\n",
       "      <th>50%</th>\n",
       "      <th>75%</th>\n",
       "      <th>max</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Region</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>Europe</th>\n",
       "      <td>1.0</td>\n",
       "      <td>4.096000</td>\n",
       "      <td>NaN</td>\n",
       "      <td>4.096</td>\n",
       "      <td>4.09600</td>\n",
       "      <td>4.0960</td>\n",
       "      <td>4.09600</td>\n",
       "      <td>4.096</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Africa</th>\n",
       "      <td>43.0</td>\n",
       "      <td>4.254581</td>\n",
       "      <td>0.682470</td>\n",
       "      <td>2.693</td>\n",
       "      <td>3.80150</td>\n",
       "      <td>4.1900</td>\n",
       "      <td>4.63450</td>\n",
       "      <td>5.872</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Asia-Pacific</th>\n",
       "      <td>43.0</td>\n",
       "      <td>5.358326</td>\n",
       "      <td>0.955062</td>\n",
       "      <td>3.462</td>\n",
       "      <td>4.65000</td>\n",
       "      <td>5.2690</td>\n",
       "      <td>6.02750</td>\n",
       "      <td>7.314</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Eastern Europe</th>\n",
       "      <td>21.0</td>\n",
       "      <td>5.498952</td>\n",
       "      <td>0.402033</td>\n",
       "      <td>4.644</td>\n",
       "      <td>5.23700</td>\n",
       "      <td>5.5690</td>\n",
       "      <td>5.83800</td>\n",
       "      <td>6.098</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Latin America</th>\n",
       "      <td>22.0</td>\n",
       "      <td>5.957818</td>\n",
       "      <td>0.750925</td>\n",
       "      <td>3.603</td>\n",
       "      <td>5.54850</td>\n",
       "      <td>6.0395</td>\n",
       "      <td>6.45400</td>\n",
       "      <td>7.079</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Western Europe</th>\n",
       "      <td>19.0</td>\n",
       "      <td>6.880474</td>\n",
       "      <td>0.611070</td>\n",
       "      <td>5.195</td>\n",
       "      <td>6.56800</td>\n",
       "      <td>6.9510</td>\n",
       "      <td>7.42300</td>\n",
       "      <td>7.537</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>North America</th>\n",
       "      <td>2.0</td>\n",
       "      <td>7.154500</td>\n",
       "      <td>0.228395</td>\n",
       "      <td>6.993</td>\n",
       "      <td>7.07375</td>\n",
       "      <td>7.1545</td>\n",
       "      <td>7.23525</td>\n",
       "      <td>7.316</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                count      mean       std    min      25%     50%      75%  \\\n",
       "Region                                                                       \n",
       "Europe            1.0  4.096000       NaN  4.096  4.09600  4.0960  4.09600   \n",
       "Africa           43.0  4.254581  0.682470  2.693  3.80150  4.1900  4.63450   \n",
       "Asia-Pacific     43.0  5.358326  0.955062  3.462  4.65000  5.2690  6.02750   \n",
       "Eastern Europe   21.0  5.498952  0.402033  4.644  5.23700  5.5690  5.83800   \n",
       "Latin America    22.0  5.957818  0.750925  3.603  5.54850  6.0395  6.45400   \n",
       "Western Europe   19.0  6.880474  0.611070  5.195  6.56800  6.9510  7.42300   \n",
       "North America     2.0  7.154500  0.228395  6.993  7.07375  7.1545  7.23525   \n",
       "\n",
       "                  max  \n",
       "Region                 \n",
       "Europe          4.096  \n",
       "Africa          5.872  \n",
       "Asia-Pacific    7.314  \n",
       "Eastern Europe  6.098  \n",
       "Latin America   7.079  \n",
       "Western Europe  7.537  \n",
       "North America   7.316  "
      ]
     },
     "execution_count": 398,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR_Region['Happiness Score'].describe().sort_values(by=\"mean\",ascending=True).head(10)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 399,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Happiness Rank</th>\n",
       "      <th>Happiness Score</th>\n",
       "      <th>Economy</th>\n",
       "      <th>Family</th>\n",
       "      <th>Health</th>\n",
       "      <th>Freedom</th>\n",
       "      <th>Generosity</th>\n",
       "      <th>Corruption</th>\n",
       "      <th>Dystopia</th>\n",
       "      <th>Job Satisfaction</th>\n",
       "      <th>Region</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Country</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>Ukraine</th>\n",
       "      <td>132</td>\n",
       "      <td>4.096</td>\n",
       "      <td>0.894652</td>\n",
       "      <td>1.394538</td>\n",
       "      <td>0.575904</td>\n",
       "      <td>0.122975</td>\n",
       "      <td>0.270061</td>\n",
       "      <td>0.023029</td>\n",
       "      <td>0.814382</td>\n",
       "      <td>72.3</td>\n",
       "      <td>Europe</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "         Happiness Rank  Happiness Score   Economy    Family    Health  \\\n",
       "Country                                                                  \n",
       "Ukraine             132            4.096  0.894652  1.394538  0.575904   \n",
       "\n",
       "          Freedom  Generosity  Corruption  Dystopia  Job Satisfaction  Region  \n",
       "Country                                                                        \n",
       "Ukraine  0.122975    0.270061    0.023029  0.814382              72.3  Europe  "
      ]
     },
     "execution_count": 399,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR[WHR[\"Region\"]==\"Europe\"].head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "WHR = WHR.replace('Europe', 'Eastern Europe')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 64,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>count</th>\n",
       "      <th>mean</th>\n",
       "      <th>std</th>\n",
       "      <th>min</th>\n",
       "      <th>25%</th>\n",
       "      <th>50%</th>\n",
       "      <th>75%</th>\n",
       "      <th>max</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Region</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>North America</th>\n",
       "      <td>2.0</td>\n",
       "      <td>7.154500</td>\n",
       "      <td>0.228395</td>\n",
       "      <td>6.993</td>\n",
       "      <td>7.07375</td>\n",
       "      <td>7.1545</td>\n",
       "      <td>7.23525</td>\n",
       "      <td>7.316</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Western Europe</th>\n",
       "      <td>19.0</td>\n",
       "      <td>6.880474</td>\n",
       "      <td>0.611070</td>\n",
       "      <td>5.195</td>\n",
       "      <td>6.56800</td>\n",
       "      <td>6.9510</td>\n",
       "      <td>7.42300</td>\n",
       "      <td>7.537</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Latin America</th>\n",
       "      <td>22.0</td>\n",
       "      <td>5.957818</td>\n",
       "      <td>0.750925</td>\n",
       "      <td>3.603</td>\n",
       "      <td>5.54850</td>\n",
       "      <td>6.0395</td>\n",
       "      <td>6.45400</td>\n",
       "      <td>7.079</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Eastern Europe</th>\n",
       "      <td>22.0</td>\n",
       "      <td>5.435182</td>\n",
       "      <td>0.493357</td>\n",
       "      <td>4.096</td>\n",
       "      <td>5.22950</td>\n",
       "      <td>5.4820</td>\n",
       "      <td>5.83475</td>\n",
       "      <td>6.098</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Asia-Pacific</th>\n",
       "      <td>43.0</td>\n",
       "      <td>5.358326</td>\n",
       "      <td>0.955062</td>\n",
       "      <td>3.462</td>\n",
       "      <td>4.65000</td>\n",
       "      <td>5.2690</td>\n",
       "      <td>6.02750</td>\n",
       "      <td>7.314</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Africa</th>\n",
       "      <td>43.0</td>\n",
       "      <td>4.254581</td>\n",
       "      <td>0.682470</td>\n",
       "      <td>2.693</td>\n",
       "      <td>3.80150</td>\n",
       "      <td>4.1900</td>\n",
       "      <td>4.63450</td>\n",
       "      <td>5.872</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                count      mean       std    min      25%     50%      75%  \\\n",
       "Region                                                                       \n",
       "North America     2.0  7.154500  0.228395  6.993  7.07375  7.1545  7.23525   \n",
       "Western Europe   19.0  6.880474  0.611070  5.195  6.56800  6.9510  7.42300   \n",
       "Latin America    22.0  5.957818  0.750925  3.603  5.54850  6.0395  6.45400   \n",
       "Eastern Europe   22.0  5.435182  0.493357  4.096  5.22950  5.4820  5.83475   \n",
       "Asia-Pacific     43.0  5.358326  0.955062  3.462  4.65000  5.2690  6.02750   \n",
       "Africa           43.0  4.254581  0.682470  2.693  3.80150  4.1900  4.63450   \n",
       "\n",
       "                  max  \n",
       "Region                 \n",
       "North America   7.316  \n",
       "Western Europe  7.537  \n",
       "Latin America   7.079  \n",
       "Eastern Europe  6.098  \n",
       "Asia-Pacific    7.314  \n",
       "Africa          5.872  "
      ]
     },
     "execution_count": 64,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR_Region['Happiness Score'].describe().sort_values(by=\"mean\",ascending=False).head(10)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 101,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "WHR_A = WHR[WHR['Region'] == 'Africa']\n",
    "WHR_WE = WHR[WHR['Region'] == 'Western Europe']\n",
    "WHR_EE = WHR[WHR['Region'] == 'Eastern Europe']\n",
    "WHR_LA = WHR[WHR['Region'] == 'Latin America']\n",
    "WHR_AP = WHR[WHR['Region'] == 'Asia-Pacific']\n",
    "WHR_NA = WHR[WHR['Region'] == 'North America']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 54,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0"
      ]
     },
     "execution_count": 54,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(WHR_A[WHR_A['Happiness Score'] > 6])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "There are 0 countries in Africa that have a happiness score above 6.0 \n"
     ]
    }
   ],
   "source": [
    "print(\"There are {} countries in Africa that have a happiness score above 6.0 \".format(len(WHR_A[WHR_A['Happiness Score'] > 6])))\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 92,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "17"
      ]
     },
     "execution_count": 92,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(WHR_WE[WHR_WE['Happiness Score'] > 6])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "There are 17 countries in Western Europe that have a happiness score above 6.0 \n"
     ]
    }
   ],
   "source": [
    "print(\"There are {} countries in Western Europe that have a happiness score above 6.0 \".format(len(WHR_WE[WHR_WE['Happiness Score'] > 6])))\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 55,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "1"
      ]
     },
     "execution_count": 55,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(WHR_EE[WHR_EE['Happiness Score'] > 6])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "There is 1 countries in Eastern Europe that have a happiness score above 6.0 \n"
     ]
    }
   ],
   "source": [
    "print(\"There is {} country in Eastern Europe that has a happiness score above 6.0 \".format(len(WHR_EE[WHR_EE['Happiness Score'] > 6])))\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 56,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "11"
      ]
     },
     "execution_count": 56,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(WHR_AP[WHR_AP['Happiness Score'] > 6])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "There are 11 countries in the Asia Pacific that have a happiness score above 6.0 \n"
     ]
    }
   ],
   "source": [
    "print(\"There are {} countries in the Asia Pacific that have a happiness score above 6.0 \".format(len(WHR_AP[WHR_AP['Happiness Score'] > 6])))\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 57,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "13"
      ]
     },
     "execution_count": 57,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(WHR_LA[WHR_LA['Happiness Score'] > 6])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "There are 13 countries in the Latin America that have a happiness score above 6.0 \n"
     ]
    }
   ],
   "source": [
    "print(\"There are {} countries in the Latin America that have a happiness score above 6.0 \".format(len(WHR_LA[WHR_LA['Happiness Score'] > 6])))\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 58,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2"
      ]
     },
     "execution_count": 58,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(WHR_NA[WHR_NA['Happiness Score'] > 6])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "There are 2 countries in the North America that have a happiness score above 6.0 \n"
     ]
    }
   ],
   "source": [
    "print(\"There are {} countries in the North America that have a happiness score above 6.0 \".format(len(WHR_NA[WHR_NA['Happiness Score'] > 6])))\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 82,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "0.322999954\n"
     ]
    }
   ],
   "source": [
    "Delta_NA = WHR_NA.max(axis=0)['Happiness Score'] - WHR_NA.min(axis=0)['Happiness Score']\n",
    "print(Delta_NA)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 60,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "2.001999855\n"
     ]
    }
   ],
   "source": [
    "Delta_EE = WHR_EE.max(axis=0)['Happiness Score'] - WHR_EE.min(axis=0)['Happiness Score']\n",
    "print(Delta_EE)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 62,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "2.342000007\n"
     ]
    }
   ],
   "source": [
    "Delta_WE = WHR_WE.max(axis=0)['Happiness Score'] - WHR_WE.min(axis=0)['Happiness Score']\n",
    "print(Delta_WE)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 64,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "3.179000139\n"
     ]
    }
   ],
   "source": [
    "Delta_A = WHR_A.max(axis=0)['Happiness Score'] - WHR_A.min(axis=0)['Happiness Score']\n",
    "print(Delta_A)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 65,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "3.47600007\n"
     ]
    }
   ],
   "source": [
    "Delta_LA = WHR_LA.max(axis=0)['Happiness Score'] - WHR_LA.min(axis=0)['Happiness Score']\n",
    "print(Delta_LA)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 66,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "3.852000237\n"
     ]
    }
   ],
   "source": [
    "Delta_AP = WHR_AP.max(axis=0)['Happiness Score'] - WHR_AP.min(axis=0)['Happiness Score']\n",
    "print(Delta_AP)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 93,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "Deltas = {}"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 95,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "Deltas[\"North America\"] = Delta_NA\n",
    "Deltas[\"Eastern Europe\"] = Delta_EE\n",
    "Deltas[\"Western Europe\"] = Delta_WE\n",
    "Deltas[\"Africa\"] = Delta_A\n",
    "Deltas[\"Latin America\"] = Delta_LA\n",
    "Deltas[\"Asia Pacific\"] = Delta_AP"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 100,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "The Asia Pacific region seems to have the largest range of happiness scores\n"
     ]
    }
   ],
   "source": [
    "print(\"The {} region seems to have the largest range of happiness scores\".format(max(Deltas, key=Deltas.get)))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "***"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## C. Bar plot of the Happiness Score\n",
    "<a id=\"plot\" > "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "1. Obtain a horizontal bar plot of the Happiness Score of the top 10 countries. Your bar chart should have the names of the countries are listed vertically along the \n",
    "y-axis and the x-axis should have labels for each number from 0 to 8. Ensure that the chart has an appropriate title and labels.\n",
    "2. You will now modify the bar chart you obtained in step 1 to turn into a stacked bar chart where the overall happiness score is divided into the seven parts corresponding to the columns:\n",
    "  * Economy\n",
    "  * Family\n",
    "  * Health\n",
    "  * Freedom\n",
    "  * Generosity\n",
    "  * Corruption\n",
    "  * Dystopia  \n",
    "  Choose a distinct color for each category and include an appropriate legend with your chart.\n",
    "3. Obtain the same stacked horizontal bar chart as in step 2 but this time instead of the top 10 countries consider all countries from the region Africa."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 422,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Text(0.5,1,u'Happiness Score of the top 10 Countries')"
      ]
     },
     "execution_count": 422,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x1a31770f90>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "WHR['Happiness Score'].head(10).plot(xticks=np.arange(9), kind='barh', figsize= (10, 10))\n",
    "plt.xlabel(\"Happiness Score\")\n",
    "plt.title('Happiness Score of the top 10 Countries')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 423,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.legend.Legend at 0x1a32372990>"
      ]
     },
     "execution_count": 423,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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KTc3N3nIkCHte/bsmdK2bduMuXPnJv7iF79IPvXUUzvn5uYm19e1kiQAAAAAlZSWlkakpqamp6ampp933nmn+cs/++yzxH/84x9ffPzxx0WvvvrqCWvXro1btmzZqlWrVq1cunRpwhtvvJH42Wefxb388stN8/LyCgsLC1dGRES4J554otn69eujx40b13rhwoWFCxYsKCoqKor3tzty5Mj2gwcP3lZUVLRy0KBB20aNGtXOf6ykpCTqo48+Kho3btyGQYMGdfztb3+7Zc2aNQWFhYXxCxcujK8ce11guhEAAABQSXXTjXJycna1bNmyXJLefPPNE95///0T0tPT0yVp3759EYWFhXFLliyxFStWJGRmZqZJ0oEDByJOOumksvfff79Rr169drdu3bpMkq644ortRUVFcZK0ZMmSRm+88cY6SRo1atT2sWPHtvX3efHFF++MiIjQmWeeua9Zs2aHevTosV+SUlJS9q9bty62T58++1XHSBIAAACAECUkJFT4t51zuu22277+7W9/uzWwzgMPPHDSL37xi22TJk3aGFg+Y8aME83ssPuMi4tzkhQZGamYmBjnL4+IiFBZWdnhNxgCphsBAAAAR+DCCy/cNWPGjOYlJSURkvTFF19Eb9y4MepnP/vZrjlz5jTZuHFjlCRt2bIlsqioKOass87a+/HHHydt3rw5srS01P71r3818bfVrVu3vdOmTWsiSVOmTGmanZ29JzxX5cNIAgAAAI5qobyyNByuuOKKXQUFBXHdu3dPlXyjDM8999wXWVlZB/7whz9sPPfcc1MqKioUHR3tJk6c+OW5556796677trUq1evtBYtWhzq2rXrvvLycpOkyZMnfzls2LDkxx577ORmzZqVTZ8+vTic12bOudproc5lZ2e7vLy8cIcBAABQKzNb7JzLbqj+8vPzizMzM7fWXhM/RH5+fvPMzMzkqo4x3QgAAABAEJIEAAAAAEFIEgAAAAAEIUkAAAAAEIQkAQAAAEAQkgQAAAAAQfidBAAAABzVJo2cl1WX7d38RP9af3dhw4YNUTfddFO7JUuWJDZu3LgsOjra3XHHHZuvueaanXUZy5F6//33E5566qlmzzzzzIY5c+YkxcbGVpx33nl766p9RhIAAACAABUVFRowYMDpOTk5e7766qvlBQUFq1588cXPN2zYEFNffR46dOiw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vpDUO6BoXMCxx+Rb2FxZl4A6fwkpcAAAAIQklFeW1qWIiAjNmjVr3U033dRuwoQJJ8fGxn73CtQ9e/ZEpqWldTYzN3bs2K/at29ftmzZslrbHDt27MbLLrvs9FatWh1KTU3dv3fv3u8SgNNPP720R48enbZt2xY9YcKE9QkJCe7CCy/c/Ze//KVVampq+m9+85uvA9uaPHnyl8OGDUt+7LHHTm7WrFnZ9OnTi+v6HtgPGYbAkYtt1dG1GjYh3GGgGsVxg8MdAqqR0aF9uENoEC8+VFZ7paPEvH6TGqyvAzsebbC+BnW4q8H6wvGr7biccIdQJ8xssXMuu6H6y8/PL87MzNzaUP2FU25ubvIll1xSMmLEiB21165b+fn5zTMzM5OrOnY8TDcCAAAAUIeO+elGAAAAwLHqlVdeKQ53DFVhJAEAAABAEJIEAAAAAEFIEgAAAAAEIUkAAAAAEISFy2GS0aax8sZdHO4wUK2ScAeAaiwPdwANZVi4AwhdWoP21r9BewNwdPjqdwuy6rK9tuNyav3dhcjIyKyOHTvuLysrs8jISPfLX/5y2x//+MctkZGRh9XX6tWrY959993EkSNHbj/SeLt165a6ZMmSwiM9/0gwkgAAAABUEhsbW1FYWLhy7dq1BfPmzSt66623Gt95552tD7edNWvWxL7wwgtNf0gsDZ0gSCQJAAAAQI3atGlTNm3atOKnn376pIqKCmVlZXVauHBhvP/4mWeemfrJJ5/Ez507NzE1NTU9NTU1PS0tLX3Hjh0Rv//979vk5eUlpqampo8dO/akffv22cCBA5NTUlLS09LS0mfPnp0kSRMnTmx27rnnnpaTk9MxOTm5y29+85tW/vYTEhK6SVJJSUlE7969U9LT09NSUlLSn3322RPr65qZbgQAAADUIj09/WBFRYU2btwYNXz48K3Tpk1r3qdPnw3Lli2LPXjwoPXs2XN///79T584ceL6888/f29JSUlEQkJCxQMPPLBx/PjxLd999921knTPPfe0lKSioqKVS5Ysibvooos6rlu3boUkLVu2rNHy5csLEhMTK7p165Z+2WWXlZx11ln7/DEkJCRUzJ07d23Tpk0rvv7666iePXumDh48eGdERN1/789IAgAAABAC55wkafjw4TveeeedxqWlpfbEE080Hzx48FZJ6tWr154777yz3f3333/S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\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x1a31770bd0>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "WHR[['Economy', 'Family','Health', 'Freedom', 'Generosity', 'Corruption', 'Dystopia']].head(10).plot(kind='barh',\n",
    "                                                                xticks=np.arange(9), stacked=True, figsize= (10, 10))\n",
    "\n",
    "plt.xlabel(\"Happiness Score\")\n",
    "plt.title('Happiness Score of the top 10 Countries')\n",
    "plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0.)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 426,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.legend.Legend at 0x1a31ff5d50>"
      ]
     },
     "execution_count": 426,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x1a31efb890>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "WHR_A[['Economy', 'Family','Health', 'Freedom', 'Generosity', 'Corruption', 'Dystopia']].head(10).plot(kind='barh',\n",
    "                                                                xticks=np.arange(9), stacked=True, figsize= (10, 10))\n",
    "\n",
    "plt.xlabel(\"Happiness Score\")\n",
    "plt.title('Happiness Score of the top 10 Countries')\n",
    "plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0.)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "***"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## D. Histogram of Job Satisfaction\n",
    "<a id=\"hist\" > "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Obtain a histogram of the Job Satisfaction using the following categories:\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 428,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Text(0.5,1,u'Distribution of Job Satisfaction')"
      ]
     },
     "execution_count": 428,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x1a31b40f50>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "WHR['Job Satisfaction'].plot(kind='hist', bins=[ 40, 50, 60, 70, 80, 90, 100], figsize=(10,10))\n",
    "\n",
    "plt.xlabel(\"Job Satisfaction in Percent\")\n",
    "plt.title(\"Distribution of Job Satisfaction\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "***"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## E. Pairwise Scatter plots\n",
    "<a id=\"scat\" > "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Obtain scatter plots of the Happiness Score versus each of the other variables. Your plots should be displayed as multiple plots table and obtained with one command as supposed to separate commands for each plot."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 429,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<seaborn.axisgrid.PairGrid at 0x1a32a5ee90>"
      ]
     },
     "execution_count": 429,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x1a3174ac10>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.pairplot(data=WHR, kind='reg', size = 5,\n",
    "                  x_vars=['Happiness Score'],\n",
    "                  y_vars=['Economy', 'Family','Health', 'Freedom', 'Generosity', 'Corruption', 'Dystopia'])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 430,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<seaborn.axisgrid.PairGrid at 0x1a28ae4e50>"
      ]
     },
     "execution_count": 430,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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AUMxm2Et3+x1zVq+OepdXYiihUE0jsRDwfZw+PuQYEpLw1WlwzB92aW4qnRY0ElFiSol1YCDu+q9rsV6qVsv/UXptNtuu633vHnzuru/vvDCCwf8/Oc/7+v++vbbb+/18MMPB127dt68ed1PnjwZkTefnTt3mtLS0kYUFBQUuv88+eST2ZF4rnBpkpkhhBgGIM/z8aSU/9LisclbImeTen5IaJv0ZDI0/64ymeg0R5MLPft3Rk316bKl7qXuWP07ufuL1tx/P6zlm2EpHhGT/qJ02o9+9KNTr7/+elcAR1wuF44dO2Y8depU6yetsrKyjKlTp+5r5yF8evrpp3Nuv/32uszMzIA3vJ1OJ4zGwH42e/fu3VRV1WZ/J0AOhwMpKSmhfGvQwv4UIYT4G4C/AZgM4Gctf34a7uOSPkS7zq5ek570KMVkwBW3DdbVUrde+ovGM1WVWaeanENVKYtPNTmHqqrM6vi7/Bs7duyp8vLyDAAoLy83Dxw40Jaenu46evSowWaziW+//TZtzJgxVsB327MTJ04ol156af+BAwcWDhgwYPCzzz7b9U9/+lP3I0eOpFxyySX5559/fj7Q3PHlvPPOKygsLBw0fvz4fu5Sgbm5uUMfeOCBnsXFxQP/9re/dR01atTAGTNm5A4dOnRQXl7ekHfffTcjmNdjsVhay4+98MILXSdPnpwHNLdg+9WvftXr/PPPzy8tLe11+PBhw2WXXXZufn5+4fDhwwu++OILMwDcd999Z0+cOPGcCy64IL9v375DFi1adJb78fy1fWuPFh9XL5BSntFUm+KfFudSKXKEImDONOGq0mEhF6KIzLia+4oCaL2lwKiqzKptaOo76+WvlLLddSjJyzItmXpe3+z0VCiKqAvlMfPy8hxGo1F+8803po8//ji9pV9oyoYNGzK6du3qHDhwoC0tLU16tj2TUuKyyy7r/84772QcPnzY2KNHD8dHH320CwBqa2sN2dnZrqeeeirn448/ru7Zs6fz4MGDxkcffbTnxo0bqzt16qQ++OCDPebPn5/zl7/85SAApKWlqeXl5TsB4LnnnuvudDrFtm3bdrz66qud582bd/a4ceOq24573759qQUFp5MkFi9evHfcuHGn2nut3377bdqnn35abTQaccstt/QePny49YMPPvh2zZo1mbfccss57pntjh07zOXl5TtO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GTD00h54b8Ui7z3QpQsxYvwEzF79BibOeajddmqRGhsRJZ9wzolKP/9NFBTPTNaOijMIRSDV4rvUoMlsbj1mE4uxEVHyCeedYLgQ4oQQ4iSAYS3/fUIIcVIIcaLD7yby4JnJ6r71J9TuL9EYGxEll5DfDaSUBillJyllppTS2PLf7q87aTnISNPbQX1qX6J3fyGi+JH0H6l99cPU8qA+ac+z1KDWe6BEichisRR1fK9ma9euzfQsFr9gwYJubasZBeKPf/xj99TU1BG1tbURK4iwevXqzr/97W8DPmcaCUn/ruOvH6YWB/UpcvRQapAoEW3YsCHzk08+yXB/PXfu3KN33313bbCP8/rrr2cPGTKkYfXq1V20HWEzh8OBG2+8sf7RRx89FInHD5QWXVzimr9+mClpXBokouiTqpqlWq25isViUq1Wu2Kx1AhF+2IL//jHPzo/9thjPR0Oh9K1a1fnq6+++p3ValVWrlzZTVEU+dprr2UvXrx47/r16ztlZGS45s2bd3jUqFEDi4uLT/3nP//pdPLkScOKFSt2jxs37lTbx66srEy1Wq3KY489tu/Pf/5zz1mzZtUCwJIlS7LXrFnTRVVVsXPnTvNdd911yG63K6+++mq2yWRS169f/01OTo6rsrIydfr06X3q6uqMaWlp6nPPPbenqKiocfLkyXldu3Z1btu2zTJs2DDr0KFDbZs2bUpfuXLl3n379hl/+ctf9t27d28qADz55JN7Lr/88obLLrvs3IMHD5qampqU6dOnH37ggQcCLnwRiKT/+B7tJBUiIn+kqma5auv67r/rLlPVsOHYf9ddJldtXV+pht9TtK3LL7/81FdffVW1Y8eO7dddd13dvHnzegwcONB+8803H50+ffrhqqqq7b4CpNPpFNu2bdvx+OOP75s3b97Zvh77pZdeypo0aVLduHHjTn3//fdpNTU1rRO26upq8z//+c/vysrKdvz5z3/OtVgs6o4dO7aPHDmy4emnn84GgF/96ld9ly9fvreysnLHwoUL98+YMaO1Rde3336b9umnn1Y/++yz+z2fc/r06X0uuuiikzt37txeWVm5fcSIEY1Aczu3ysrKHV999dX2p59+OufQoUOaLi8nfRBlkgoFqm3he6nyZBdpS7XwMuEcAAAgAElEQVRac2seuF+xfvEl4HTC+sWXqHngfkW1WnO1fq7vv//edNFFFw3Iz88vXLJkSY+qqqqADj9PmTLlGACMGTOmYf/+/T67y7zxxhtZN998c53BYMD48eOPrVy5sqv778aMGXOya9eu6tlnn+3MyMhwTZky5TgADB061Lp79+7U+vp6paKiImPKlCnnFhQUFJaWlvY9cuRIivv7J02adMxoPHMR9bPPPsucM2fOUQAwGo3Izs52Ac3t3AYOHFhYXFw8yN3OLYh/pg4l/XJue/0widxiWYtWlWrr+VSeU01sisVispZv9rpmLd8MxWIJuRWaP3fffXefe+6559CNN95Yv3bt2kx/s8q20tLSJNAcqFwu1xk//F988YV5z549qePGjcsHAIfDIXr37t30m9/85igAmEym1k+fiqK0Pp6iKHA6ncLlciEzM9NZVdVmn61FRkZGwFmfnu3cMjMz1VGjRg202Wya/vLwNxFMUolnobQpC0Ws+nN21EVGVSVO/X/27j0+qvLOH/jnOXPJzIRwCSLQACJCwASwIQmsN2qpWgSL190t9dYu3hoJ6080v/3Vutuf7u5rG8quTSparVd+Xl62Xa0VUNrFirdqEtKCQUSgVAiCkYEQMvc5z++PZMaZMDOZOXPmcmY+79eL1zGHycwzmMz3PM/5Pt+vNwBVDh45OzY01eXyOWrnRZ1z1M6D6nJpboUWT19fn2nKlCl+AHjqqafC2bdlZWXBvr4+zUuezzzzTPnq1asPdXd37+ju7t7x+eefbz98+LB19+7dSV0IlJeXq5MmTfI98cQTYwBAVVW89957w86Szz///L41a9aMA4BAIACn06nEa+emJ0YLMqx02pSlKlF/zkwu67oDbjRtbULb4TYEZABth9vQtLUJ7oAbqipxtN+HW55uR+W9m3DL0+042u9jIDUwxeHorvjJWtWxYD5gNsOxYD4qfrJWVRwOza3QAMDj8Sjjx4+fG/rzox/9aPy99957aPny5WfV1tbOHDt2bCD02Guuueb4hg0bRs+aNavqtddeG5HoeWN5+eWXy//u7/7ueOS5yy677NjTTz+d9H3d559/ft+TTz552syZM6tmzJhR/etf/3rYDN+HH3740zfffLOssrKyavbs2VXbtm2zp9vOLRlpt0LLJ2yFVlz0alOWjFgt2CoqR+Oi62fBMdIKqy0zd0ZUqaJ2fS0CMvwZB7Mwo+OGDrh8Km55uh3v7fty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zg1eJOneCs3lcikAMGHChEBvb6/y29/+dgwABINB7N271/qtb32rb926dQf7+vpMvb29pqEt0i644IITP/7xj8PFq999992MXFGeccYZvo6ODgcAPPvss6MDgUDMALxo0aKTGzduHN3X16ecOHFC2bhx45ivf/3rfQDw2WefWX//+9+XAsBzzz1Xft55552cO3eux+l0mkPnvV6vaG9vT/lKn8u5lBGhHq0ADLuEO1Qus6CHNo/3uQe2D53zjdHMzi0gZqup+9IV1WdsfrxLiWj+rpqtprRaoYXuiYa+XrRoUe+6deu6r7vuup6qqqrqSZMm+UJtwgKBgPjOd75zZl9fn0lKKW677bYjp512WvCaa645fu211561adOm0Q8++OCnjz766IGbb755SmVlZVUwGBQLFizoO++88z5NZ5w33njjtNAWl/Ly8sC77767u7Gxsefyyy+fPmfOnLMXLlx4wm63x+ywccEFF7i+853vHJ03b97ZAHDDDTf0nH/++e6PP/7YOm3aNM8TTzwxtqGh4YwzzzzTe/fdd/fYbDb5wgsv7F21atWUvr4+UzAYFN///veP1NXVpZQByVZoRESZoakVmqrK8oAvWGEpMVn93qDPbDV1K4pgJxeNPv74Y+vll18+45NPPunS4/mGtkLjTJSIKI8oinCGkohYUCP/GfcmFRER0TBmzpzp02sWGguDKBERkUYMokQ6SNRphYgKFxfcidIU6rSy+fEuRGRUwl5mZdYsUYHjTJQohlRmlpGdVlRVhjutsBQfUeFjECUaItUenpGdVkJYio/yzTPPPDNaCFHb2dkZLihw2223TZo+fXp1rDq1zz777Kgf/OAHE7I7SuPJyXKuEGIxgJ8CMAH4hZTyP4b8/V0AbgYQANAD4B+klH/N+kCpKKXawzPUaSX0eCBcZYZbFChvvPDCC+Xz5s07uX79+vKamppDAPDss8+O6+np+ZPdbo+6QvT7/bjuuut6AfTGfDIKy/pMVAhhAvAQgMsAVAFYLoSoGvKwTgB1Usq5AH4FoDm7o6RMUKWKfn9/1DEfpTqzDHVaqagcDUURqKgczVJ8pJmqquU+t2uOlGqtz+2ao6pq2q3Qent7lfb29hFPPvnk/pdeemkMACxatGi62+1Wampqzn7sscfGXHPNNVNvvvnmSQsWLKhsaGiY1NLSMvbGG2+cAgAH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\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x1a28ae4f90>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.pairplot(data=WHR, size = 5, hue='Region',\n",
    "                  x_vars=['Happiness Score'],\n",
    "                  y_vars=['Economy', 'Family','Health', 'Freedom', 'Generosity', 'Corruption', 'Dystopia'])"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "***"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## F. Correlation\n",
    "<a id=\"corr\" > "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Obtain the correlation between the Happiness Score and each of the other variables. Which variable has the highest correlation with the Happiness Score?"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 431,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Happiness Score     1.000000\n",
       "Job Satisfaction    0.812873\n",
       "Economy             0.808678\n",
       "Health              0.777731\n",
       "Family              0.749612\n",
       "Freedom             0.567948\n",
       "Dystopia            0.481117\n",
       "Corruption          0.438262\n",
       "Generosity          0.164123\n",
       "Happiness Rank     -0.992663\n",
       "Name: Happiness Score, dtype: float64"
      ]
     },
     "execution_count": 431,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR.corr(method=\"pearson\", min_periods=20)[\"Happiness Score\"].sort_values(ascending=False)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 52,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Happiness Score     1.000000\n",
       "Happiness Rank      0.992782\n",
       "Job Satisfaction    0.812873\n",
       "Economy             0.811194\n",
       "Health              0.780496\n",
       "Family              0.753815\n",
       "Freedom             0.576027\n",
       "Dystopia            0.474300\n",
       "Corruption          0.435854\n",
       "Generosity          0.160010\n",
       "Name: Happiness Score, dtype: float64"
      ]
     },
     "execution_count": 52,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR.corr(method=\"pearson\", min_periods=20)[\"Happiness Score\"].abs().sort_values(ascending=False)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "If we ignore the Happiness Rank, Job Satisfaction seems to have the highest correlation with the Happiness Score."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 432,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Happiness Rank</th>\n",
       "      <th>Happiness Score</th>\n",
       "      <th>Economy</th>\n",
       "      <th>Family</th>\n",
       "      <th>Health</th>\n",
       "      <th>Freedom</th>\n",
       "      <th>Generosity</th>\n",
       "      <th>Corruption</th>\n",
       "      <th>Dystopia</th>\n",
       "      <th>Job Satisfaction</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>Happiness Rank</th>\n",
       "      <td>1.000000</td>\n",
       "      <td>-0.992663</td>\n",
       "      <td>-0.809521</td>\n",
       "      <td>-0.733902</td>\n",
       "      <td>-0.776602</td>\n",
       "      <td>-0.550111</td>\n",
       "      <td>-0.142348</td>\n",
       "      <td>-0.415532</td>\n",
       "      <td>-0.489194</td>\n",
       "      <td>-0.814535</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Happiness Score</th>\n",
       "      <td>-0.992663</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.808678</td>\n",
       "      <td>0.749612</td>\n",
       "      <td>0.777731</td>\n",
       "      <td>0.567948</td>\n",
       "      <td>0.164123</td>\n",
       "      <td>0.438262</td>\n",
       "      <td>0.481117</td>\n",
       "      <td>0.812873</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Economy</th>\n",
       "      <td>-0.809521</td>\n",
       "      <td>0.808678</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.685524</td>\n",
       "      <td>0.838884</td>\n",
       "      <td>0.363843</td>\n",
       "      <td>-0.015614</td>\n",
       "      <td>0.358750</td>\n",
       "      <td>0.022620</td>\n",
       "      <td>0.700662</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Family</th>\n",
       "      <td>-0.733902</td>\n",
       "      <td>0.749612</td>\n",
       "      <td>0.685524</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.606674</td>\n",
       "      <td>0.412633</td>\n",
       "      <td>0.050771</td>\n",
       "      <td>0.236262</td>\n",
       "      <td>0.075480</td>\n",
       "      <td>0.623266</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Health</th>\n",
       "      <td>-0.776602</td>\n",
       "      <td>0.777731</td>\n",
       "      <td>0.838884</td>\n",
       "      <td>0.606674</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.340986</td>\n",
       "      <td>0.068895</td>\n",
       "      <td>0.286777</td>\n",
       "      <td>0.055886</td>\n",
       "      <td>0.704795</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Freedom</th>\n",
       "      <td>-0.550111</td>\n",
       "      <td>0.567948</td>\n",
       "      <td>0.363843</td>\n",
       "      <td>0.412633</td>\n",
       "      <td>0.340986</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.319387</td>\n",
       "      <td>0.501632</td>\n",
       "      <td>0.092923</td>\n",
       "      <td>0.500655</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Generosity</th>\n",
       "      <td>-0.142348</td>\n",
       "      <td>0.164123</td>\n",
       "      <td>-0.015614</td>\n",
       "      <td>0.050771</td>\n",
       "      <td>0.068895</td>\n",
       "      <td>0.319387</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.292363</td>\n",
       "      <td>-0.102683</td>\n",
       "      <td>0.220032</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Corruption</th>\n",
       "      <td>-0.415532</td>\n",
       "      <td>0.438262</td>\n",
       "      <td>0.358750</td>\n",
       "      <td>0.236262</td>\n",
       "      <td>0.286777</td>\n",
       "      <td>0.501632</td>\n",
       "      <td>0.292363</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>-0.014995</td>\n",
       "      <td>0.337131</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Dystopia</th>\n",
       "      <td>-0.489194</td>\n",
       "      <td>0.481117</td>\n",
       "      <td>0.022620</td>\n",
       "      <td>0.075480</td>\n",
       "      <td>0.055886</td>\n",
       "      <td>0.092923</td>\n",
       "      <td>-0.102683</td>\n",
       "      <td>-0.014995</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.281655</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Job Satisfaction</th>\n",
       "      <td>-0.814535</td>\n",
       "      <td>0.812873</td>\n",
       "      <td>0.700662</td>\n",
       "      <td>0.623266</td>\n",
       "      <td>0.704795</td>\n",
       "      <td>0.500655</td>\n",
       "      <td>0.220032</td>\n",
       "      <td>0.337131</td>\n",
       "      <td>0.281655</td>\n",
       "      <td>1.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                  Happiness Rank  Happiness Score   Economy    Family  \\\n",
       "Happiness Rank          1.000000        -0.992663 -0.809521 -0.733902   \n",
       "Happiness Score        -0.992663         1.000000  0.808678  0.749612   \n",
       "Economy                -0.809521         0.808678  1.000000  0.685524   \n",
       "Family                 -0.733902         0.749612  0.685524  1.000000   \n",
       "Health                 -0.776602         0.777731  0.838884  0.606674   \n",
       "Freedom                -0.550111         0.567948  0.363843  0.412633   \n",
       "Generosity             -0.142348         0.164123 -0.015614  0.050771   \n",
       "Corruption             -0.415532         0.438262  0.358750  0.236262   \n",
       "Dystopia               -0.489194         0.481117  0.022620  0.075480   \n",
       "Job Satisfaction       -0.814535         0.812873  0.700662  0.623266   \n",
       "\n",
       "                    Health   Freedom  Generosity  Corruption  Dystopia  \\\n",
       "Happiness Rank   -0.776602 -0.550111   -0.142348   -0.415532 -0.489194   \n",
       "Happiness Score   0.777731  0.567948    0.164123    0.438262  0.481117   \n",
       "Economy           0.838884  0.363843   -0.015614    0.358750  0.022620   \n",
       "Family            0.606674  0.412633    0.050771    0.236262  0.075480   \n",
       "Health            1.000000  0.340986    0.068895    0.286777  0.055886   \n",
       "Freedom           0.340986  1.000000    0.319387    0.501632  0.092923   \n",
       "Generosity        0.068895  0.319387    1.000000    0.292363 -0.102683   \n",
       "Corruption        0.286777  0.501632    0.292363    1.000000 -0.014995   \n",
       "Dystopia          0.055886  0.092923   -0.102683   -0.014995  1.000000   \n",
       "Job Satisfaction  0.704795  0.500655    0.220032    0.337131  0.281655   \n",
       "\n",
       "                  Job Satisfaction  \n",
       "Happiness Rank           -0.814535  \n",
       "Happiness Score           0.812873  \n",
       "Economy                   0.700662  \n",
       "Family                    0.623266  \n",
       "Health                    0.704795  \n",
       "Freedom                   0.500655  \n",
       "Generosity                0.220032  \n",
       "Corruption                0.337131  \n",
       "Dystopia                  0.281655  \n",
       "Job Satisfaction          1.000000  "
      ]
     },
     "execution_count": 432,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR.corr(method=\"pearson\", min_periods=20)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 433,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x1a2a05f550>"
      ]
     },
     "execution_count": 433,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x117500050>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "corr = WHR.corr(method = \"pearson\")\n",
    "\n",
    "f, ax = plt.subplots(figsize=(10, 10))\n",
    "\n",
    "sns.heatmap(corr, mask=np.zeros_like(corr, dtype=np.bool), \n",
    "            cmap=sns.diverging_palette(220, 10, as_cmap=True), square=True, ax=ax)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "***"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## G. Probabilities\n",
    "<a id=\"prob\" > "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Compute the probability that randomly selected country with Happiness score over 6.0 is from Western Europe. You will have to use pandas to count the appropriate quantities."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "44"
      ]
     },
     "execution_count": 27,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR[WHR['Happiness Score'] > 6].shape[0]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "17"
      ]
     },
     "execution_count": 29,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR[(WHR['Happiness Score'] > 6) & (WHR['Region'] == 'Western Europe')].shape[0]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 437,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.38636363636363635"
      ]
     },
     "execution_count": 437,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "float(len(WHR[(WHR['Happiness Score'] > 6) & (WHR['Region'] == 'Western Europe')]))/float(len(WHR[WHR['Happiness Score'] > 6]))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 51,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "The probability that a randomly selected country with Happiness scoee over 6.0 is form Western Europe is 39%\n"
     ]
    }
   ],
   "source": [
    "print(\"The probability that a randomly selected country with happiness score over 6.0 is form Western Europe is {0:.0%}\".format(float(WHR[(WHR['Happiness Score'] > 6) & (WHR['Region'] == 'Western Europe')].shape[0]\n",
    "\n",
    ")/float(WHR[WHR['Happiness Score'] > 6].shape[0])))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "***"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## H. Matrices\n",
    "<a id=\"mat\" > "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Define a matrix whose rows correspond to countries and the columns to the regions. Fill in the matrix with 0/1 values where entry (i,j) is a 1 if the country in row i is in the region in column j and a 0 otherwise."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 438,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(151, 11)"
      ]
     },
     "execution_count": 438,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "WHR.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 439,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "Western_Europe = []\n",
    "Eastern_Europe = []\n",
    "North_America = []\n",
    "Latin_America = []\n",
    "Asia_Pacific = []\n",
    "Africa = []"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 440,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "for x in WHR['Region']:\n",
    "    if x == 'Western Europe':\n",
    "         Western_Europe.append(1)\n",
    "    else: Western_Europe.append(0)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 441,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "for x in WHR['Region']:\n",
    "    if x == 'Eastern Europe':\n",
    "         Eastern_Europe.append(1)\n",
    "    else: Eastern_Europe.append(0)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 442,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "for x in WHR['Region']:\n",
    "    if x == 'North America':\n",
    "         North_America.append(1)\n",
    "    else: North_America.append(0)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 443,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "for x in WHR['Region']:\n",
    "    if x == 'Latin America':\n",
    "         Latin_America.append(1)\n",
    "    else: Latin_America.append(0)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 445,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "for x in WHR['Region']:\n",
    "    if x == 'Asia-Pacific':\n",
    "         Asia_Pacific.append(1)\n",
    "    else: Asia_Pacific.append(0)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 446,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "for x in WHR['Region']:\n",
    "    if x == 'Africa':\n",
    "         Africa.append(1)\n",
    "    else: Africa.append(0)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 447,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "Matrix = pd.DataFrame(index=WHR.index)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 448,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "Matrix['Western Europe'] = Western_Europe\n",
    "Matrix['Eastern Europe'] = Eastern_Europe\n",
    "Matrix['North America'] = North_America\n",
    "Matrix['Latin America'] = Latin_America\n",
    "Matrix['Asia Pacific'] = Asia_Pacific\n",
    "Matrix['Africa'] = Africa"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 450,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Western Europe</th>\n",
       "      <th>Eastern Europe</th>\n",
       "      <th>North America</th>\n",
       "      <th>Latin America</th>\n",
       "      <th>Asia Pacific</th>\n",
       "      <th>Africa</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Country</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>Norway</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Denmark</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Iceland</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Switzerland</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Finland</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Netherlands</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Canada</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>New Zealand</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Sweden</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Australia</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Israel</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Costa Rica</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Austria</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>United States</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Ireland</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Germany</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Belgium</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Luxembourg</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>United Kingdom</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Chile</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                Western Europe  Eastern Europe  North America  Latin America  \\\n",
       "Country                                                                        \n",
       "Norway                       1               0              0              0   \n",
       "Denmark                      1               0              0              0   \n",
       "Iceland                      1               0              0              0   \n",
       "Switzerland                  1               0              0              0   \n",
       "Finland                      1               0              0              0   \n",
       "Netherlands                  1               0              0              0   \n",
       "Canada                       0               0              1              0   \n",
       "New Zealand                  0               0              0              0   \n",
       "Sweden                       1               0              0              0   \n",
       "Australia                    0               0              0              0   \n",
       "Israel                       0               0              0              0   \n",
       "Costa Rica                   0               0              0              1   \n",
       "Austria                      1               0              0              0   \n",
       "United States                0               0              1              0   \n",
       "Ireland                      1               0              0              0   \n",
       "Germany                      1               0              0              0   \n",
       "Belgium                      1               0              0              0   \n",
       "Luxembourg                   1               0              0              0   \n",
       "United Kingdom               1               0              0              0   \n",
       "Chile                        0               0              0              1   \n",
       "\n",
       "                Asia Pacific  Africa  \n",
       "Country                               \n",
       "Norway                     0       0  \n",
       "Denmark                    0       0  \n",
       "Iceland                    0       0  \n",
       "Switzerland                0       0  \n",
       "Finland                    0       0  \n",
       "Netherlands                0       0  \n",
       "Canada                     0       0  \n",
       "New Zealand                1       0  \n",
       "Sweden                     0       0  \n",
       "Australia                  1       0  \n",
       "Israel                     1       0  \n",
       "Costa Rica                 0       0  \n",
       "Austria                    0       0  \n",
       "United States              0       0  \n",
       "Ireland                    0       0  \n",
       "Germany                    0       0  \n",
       "Belgium                    0       0  \n",
       "Luxembourg                 0       0  \n",
       "United Kingdom             0       0  \n",
       "Chile                      0       0  "
      ]
     },
     "execution_count": 450,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Matrix.head(20)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 451,
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "array_Matrix = Matrix.as_matrix()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 452,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([[1, 0, 0, 0, 0, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [0, 0, 1, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [0, 0, 1, 0, 0, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [1, 0, 0, 0, 0, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 1, 0, 0, 0, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 1, 0, 0],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 1, 0],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1],\n",
       "       [0, 0, 0, 0, 0, 1]])"
      ]
     },
     "execution_count": 452,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "array_Matrix"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 2",
   "language": "python",
   "name": "python2"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 2
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython2",
   "version": "2.7.14"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
