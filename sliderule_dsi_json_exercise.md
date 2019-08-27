
# JSON examples and exercise
****
+ get familiar with packages for dealing with JSON
+ study examples with JSON strings and files 
+ work on exercise to be completed and submitted 
****
+ reference: http://pandas.pydata.org/pandas-docs/stable/io.html#io-json-reader
+ data source: http://jsonstudio.com/resources/
****


```python
import pandas as pd
import numpy as np
```

## imports for Python, Pandas


```python
import json
from pandas.io.json import json_normalize
```

## JSON example, with string

+ demonstrates creation of normalized dataframes (tables) from nested json string
+ source: http://pandas.pydata.org/pandas-docs/stable/io.html#normalization


```python
# define json string
data = [{'state': 'Florida', 
         'shortname': 'FL',
         'info': {'governor': 'Rick Scott'},
         'counties': [{'name': 'Dade', 'population': 12345},
                      {'name': 'Broward', 'population': 40000},
                      {'name': 'Palm Beach', 'population': 60000}]},
        {'state': 'Ohio',
         'shortname': 'OH',
         'info': {'governor': 'John Kasich'},
         'counties': [{'name': 'Summit', 'population': 1234},
                      {'name': 'Cuyahoga', 'population': 1337}]}]
```


```python
# use normalization to create tables from nested element
json_normalize(data, 'counties')
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
      <th>name</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Dade</td>
      <td>12345</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Broward</td>
      <td>40000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Palm Beach</td>
      <td>60000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Summit</td>
      <td>1234</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Cuyahoga</td>
      <td>1337</td>
    </tr>
  </tbody>
</table>
</div>




```python
# further populate tables created from nested element
json_normalize(data, 'counties', ['state', 'shortname', ['info', 'governor']])
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
      <th>name</th>
      <th>population</th>
      <th>state</th>
      <th>shortname</th>
      <th>info.governor</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Dade</td>
      <td>12345</td>
      <td>Florida</td>
      <td>FL</td>
      <td>Rick Scott</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Broward</td>
      <td>40000</td>
      <td>Florida</td>
      <td>FL</td>
      <td>Rick Scott</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Palm Beach</td>
      <td>60000</td>
      <td>Florida</td>
      <td>FL</td>
      <td>Rick Scott</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Summit</td>
      <td>1234</td>
      <td>Ohio</td>
      <td>OH</td>
      <td>John Kasich</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Cuyahoga</td>
      <td>1337</td>
      <td>Ohio</td>
      <td>OH</td>
      <td>John Kasich</td>
    </tr>
  </tbody>
</table>
</div>



****
## JSON example, with file

+ demonstrates reading in a json file as a string and as a table
+ uses small sample file containing data about projects funded by the World Bank 
+ data source: http://jsonstudio.com/resources/


```python
# load json as string
json.load((open('world_bank_projects_less.json')))
```




    [{'_id': {'$oid': '52b213b38594d8a2be17c780'},
      'approvalfy': 1999,
      'board_approval_month': 'November',
      'boardapprovaldate': '2013-11-12T00:00:00Z',
      'borrower': 'FEDERAL DEMOCRATIC REPUBLIC OF ETHIOPIA',
      'closingdate': '2018-07-07T00:00:00Z',
      'country_namecode': 'Federal Democratic Republic of Ethiopia!$!ET',
      'countrycode': 'ET',
      'countryname': 'Federal Democratic Republic of Ethiopia',
      'countryshortname': 'Ethiopia',
      'docty': 'Project Information Document,Indigenous Peoples Plan,Project Information Document',
      'envassesmentcategorycode': 'C',
      'grantamt': 0,
      'ibrdcommamt': 0,
      'id': 'P129828',
      'idacommamt': 130000000,
      'impagency': 'MINISTRY OF EDUCATION',
      'lendinginstr': 'Investment Project Financing',
      'lendinginstrtype': 'IN',
      'lendprojectcost': 550000000,
      'majorsector_percent': [{'Name': 'Education', 'Percent': 46},
       {'Name': 'Education', 'Percent': 26},
       {'Name': 'Public Administration, Law, and Justice', 'Percent': 16},
       {'Name': 'Education', 'Percent': 12}],
      'mjsector_namecode': [{'name': 'Education', 'code': 'EX'},
       {'name': 'Education', 'code': 'EX'},
       {'name': 'Public Administration, Law, and Justice', 'code': 'BX'},
       {'name': 'Education', 'code': 'EX'}],
      'mjtheme': ['Human development'],
      'mjtheme_namecode': [{'name': 'Human development', 'code': '8'},
       {'name': '', 'code': '11'}],
      'mjthemecode': '8,11',
      'prodline': 'PE',
      'prodlinetext': 'IBRD/IDA',
      'productlinetype': 'L',
      'project_abstract': {'cdata': 'The development objective of the Second Phase of General Education Quality Improvement Project for Ethiopia is to improve learning conditions in primary and secondary schools and strengthen institutions at different levels of educational administration. The project has six components. The first component is curriculum, textbooks, assessment, examinations, and inspection. This component will support improvement of learning conditions in grades KG-12 by providing increased access to teaching and learning materials and through improvements to the curriculum by assessing the strengths and weaknesses of the current curriculum. This component has following four sub-components: (i) curriculum reform and implementation; (ii) teaching and learning materials; (iii) assessment and examinations; and (iv) inspection. The second component is teacher development program (TDP). This component will support improvements in learning conditions in both primary and secondary schools by advancing the quality of teaching in general education through: (a) enhancing the training of pre-service teachers in teacher education institutions; and (b) improving the quality of in-service teacher training. This component has following three sub-components: (i) pre-service teacher training; (ii) in-service teacher training; and (iii) licensing and relicensing of teachers and school leaders. The third component is school improvement plan. This component will support the strengthening of school planning in order to improve learning outcomes, and to partly fund the school improvement plans through school grants. It has following two sub-components: (i) school improvement plan; and (ii) school grants. The fourth component is management and capacity building, including education management information systems (EMIS). This component will support management and capacity building aspect of the project. This component has following three sub-components: (i) capacity building for education planning and management; (ii) capacity building for school planning and management; and (iii) EMIS. The fifth component is improving the quality of learning and teaching in secondary schools and universities through the use of information and communications technology (ICT). It has following five sub-components: (i) national policy and institution for ICT in general education; (ii) national ICT infrastructure improvement plan for general education; (iii) develop an integrated monitoring, evaluation, and learning system specifically for the ICT component; (iv) teacher professional development in the use of ICT; and (v) provision of limited number of e-Braille display readers with the possibility to scale up to all secondary education schools based on the successful implementation and usage of the readers. The sixth component is program coordination, monitoring and evaluation, and communication. It will support institutional strengthening by developing capacities in all aspects of program coordination, monitoring and evaluation; a new sub-component on communications will support information sharing for better management and accountability. It has following three sub-components: (i) program coordination; (ii) monitoring and evaluation (M and E); and (iii) communication.'},
      'project_name': 'Ethiopia General Education Quality Improvement Project II',
      'projectdocs': [{'DocTypeDesc': 'Project Information Document (PID),  Vol.',
        'DocType': 'PID',
        'EntityID': '090224b081e545fb_1_0',
        'DocURL': 'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=090224b081e545fb_1_0',
        'DocDate': '28-AUG-2013'},
       {'DocTypeDesc': 'Indigenous Peoples Plan (IP),  Vol.1 of 1',
        'DocType': 'IP',
        'EntityID': '000442464_20130920111729',
        'DocURL': 'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000442464_20130920111729',
        'DocDate': '01-JUL-2013'},
       {'DocTypeDesc': 'Project Information Document (PID),  Vol.',
        'DocType': 'PID',
        'EntityID': '090224b0817b19e2_1_0',
        'DocURL': 'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=090224b0817b19e2_1_0',
        'DocDate': '22-NOV-2012'}],
      'projectfinancialtype': 'IDA',
      'projectstatusdisplay': 'Active',
      'regionname': 'Africa',
      'sector': [{'Name': 'Primary education'},
       {'Name': 'Secondary education'},
       {'Name': 'Public administration- Other social services'},
       {'Name': 'Tertiary education'}],
      'sector1': {'Name': 'Primary education', 'Percent': 46},
      'sector2': {'Name': 'Secondary education', 'Percent': 26},
      'sector3': {'Name': 'Public administration- Other social services',
       'Percent': 16},
      'sector4': {'Name': 'Tertiary education', 'Percent': 12},
      'sector_namecode': [{'name': 'Primary education', 'code': 'EP'},
       {'name': 'Secondary education', 'code': 'ES'},
       {'name': 'Public administration- Other social services', 'code': 'BS'},
       {'name': 'Tertiary education', 'code': 'ET'}],
      'sectorcode': 'ET,BS,ES,EP',
      'source': 'IBRD',
      'status': 'Active',
      'supplementprojectflg': 'N',
      'theme1': {'Name': 'Education for all', 'Percent': 100},
      'theme_namecode': [{'name': 'Education for all', 'code': '65'}],
      'themecode': '65',
      'totalamt': 130000000,
      'totalcommamt': 130000000,
      'url': 'http://www.worldbank.org/projects/P129828/ethiopia-general-education-quality-improvement-project-ii?lang=en'},
     {'_id': {'$oid': '52b213b38594d8a2be17c781'},
      'approvalfy': 2015,
      'board_approval_month': 'November',
      'boardapprovaldate': '2013-11-04T00:00:00Z',
      'borrower': 'GOVERNMENT OF TUNISIA',
      'country_namecode': 'Republic of Tunisia!$!TN',
      'countrycode': 'TN',
      'countryname': 'Republic of Tunisia',
      'countryshortname': 'Tunisia',
      'docty': 'Project Information Document,Integrated Safeguards Data Sheet,Integrated Safeguards Data Sheet,Project Information Document,Integrated Safeguards Data Sheet,Project Information Document',
      'envassesmentcategorycode': 'C',
      'grantamt': 4700000,
      'ibrdcommamt': 0,
      'id': 'P144674',
      'idacommamt': 0,
      'impagency': 'MINISTRY OF FINANCE',
      'lendinginstr': 'Specific Investment Loan',
      'lendinginstrtype': 'IN',
      'lendprojectcost': 5700000,
      'majorsector_percent': [{'Name': 'Public Administration, Law, and Justice',
        'Percent': 70},
       {'Name': 'Public Administration, Law, and Justice', 'Percent': 30}],
      'mjsector_namecode': [{'name': 'Public Administration, Law, and Justice',
        'code': 'BX'},
       {'name': 'Public Administration, Law, and Justice', 'code': 'BX'}],
      'mjtheme': ['Economic management', 'Social protection and risk management'],
      'mjtheme_namecode': [{'name': 'Economic management', 'code': '1'},
       {'name': 'Social protection and risk management', 'code': '6'}],
      'mjthemecode': '1,6',
      'prodline': 'RE',
      'prodlinetext': 'Recipient Executed Activities',
      'productlinetype': 'L',
      'project_name': 'TN: DTF Social Protection Reforms Support',
      'projectdocs': [{'DocTypeDesc': 'Project Information Document (PID),  Vol.1 of 1',
        'DocType': 'PID',
        'EntityID': '000333037_20131024115616',
        'DocURL': 'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000333037_20131024115616',
        'DocDate': '29-MAR-2013'},
       {'DocTypeDesc': 'Integrated Safeguards Data Sheet (ISDS),  Vol.1 of 1',
        'DocType': 'ISDS',
        'EntityID': '000356161_20131024151611',
        'DocURL': 'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000356161_20131024151611',
        'DocDate': '29-MAR-2013'},
       {'DocTypeDesc': 'Integrated Safeguards Data Sheet (ISDS),  Vol.1 of 1',
        'DocType': 'ISDS',
        'EntityID': '000442464_20131031112136',
        'DocURL': 'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000442464_20131031112136',
        'DocDate': '29-MAR-2013'},
       {'DocTypeDesc': 'Project Information Document (PID),  Vol.1 of 1',
        'DocType': 'PID',
        'EntityID': '000333037_20131031105716',
        'DocURL': 'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000333037_20131031105716',
        'DocDate': '29-MAR-2013'},
       {'DocTypeDesc': 'Integrated Safeguards Data Sheet (ISDS),  Vol.1 of 1',
        'DocType': 'ISDS',
        'EntityID': '000356161_20130305113209',
        'DocURL': 'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000356161_20130305113209',
        'DocDate': '16-JAN-2013'},
       {'DocTypeDesc': 'Project Information Document (PID),  Vol.1 of 1',
        'DocType': 'PID',
        'EntityID': '000356161_20130305113716',
        'DocURL': 'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000356161_20130305113716',
        'DocDate': '16-JAN-2013'}],
      'projectfinancialtype': 'OTHER',
      'projectstatusdisplay': 'Active',
      'regionname': 'Middle East and North Africa',
      'sector': [{'Name': 'Public administration- Other social services'},
       {'Name': 'General public administration sector'}],
      'sector1': {'Name': 'Public administration- Other social services',
       'Percent': 70},
      'sector2': {'Name': 'General public administration sector', 'Percent': 30},
      'sector_namecode': [{'name': 'Public administration- Other social services',
        'code': 'BS'},
       {'name': 'General public administration sector', 'code': 'BZ'}],
      'sectorcode': 'BZ,BS',
      'source': 'IBRD',
      'status': 'Active',
      'supplementprojectflg': 'N',
      'theme1': {'Name': 'Other economic management', 'Percent': 30},
      'theme_namecode': [{'name': 'Other economic management', 'code': '24'},
       {'name': 'Social safety nets', 'code': '54'}],
      'themecode': '54,24',
      'totalamt': 0,
      'totalcommamt': 4700000,
      'url': 'http://www.worldbank.org/projects/P144674?lang=en'}]




```python
# load as Pandas dataframe
sample_json_df = pd.read_json('world_bank_projects_less.json')
sample_json_df
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
      <th>_id</th>
      <th>approvalfy</th>
      <th>board_approval_month</th>
      <th>boardapprovaldate</th>
      <th>borrower</th>
      <th>closingdate</th>
      <th>country_namecode</th>
      <th>countrycode</th>
      <th>countryname</th>
      <th>countryshortname</th>
      <th>...</th>
      <th>sectorcode</th>
      <th>source</th>
      <th>status</th>
      <th>supplementprojectflg</th>
      <th>theme1</th>
      <th>theme_namecode</th>
      <th>themecode</th>
      <th>totalamt</th>
      <th>totalcommamt</th>
      <th>url</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>{'$oid': '52b213b38594d8a2be17c780'}</td>
      <td>1999</td>
      <td>November</td>
      <td>2013-11-12T00:00:00Z</td>
      <td>FEDERAL DEMOCRATIC REPUBLIC OF ETHIOPIA</td>
      <td>2018-07-07T00:00:00Z</td>
      <td>Federal Democratic Republic of Ethiopia!$!ET</td>
      <td>ET</td>
      <td>Federal Democratic Republic of Ethiopia</td>
      <td>Ethiopia</td>
      <td>...</td>
      <td>ET,BS,ES,EP</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Name': 'Education for all', 'Percent': 100}</td>
      <td>[{'name': 'Education for all', 'code': '65'}]</td>
      <td>65</td>
      <td>130000000</td>
      <td>130000000</td>
      <td>http://www.worldbank.org/projects/P129828/ethi...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>{'$oid': '52b213b38594d8a2be17c781'}</td>
      <td>2015</td>
      <td>November</td>
      <td>2013-11-04T00:00:00Z</td>
      <td>GOVERNMENT OF TUNISIA</td>
      <td>NaN</td>
      <td>Republic of Tunisia!$!TN</td>
      <td>TN</td>
      <td>Republic of Tunisia</td>
      <td>Tunisia</td>
      <td>...</td>
      <td>BZ,BS</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Name': 'Other economic management', 'Percent...</td>
      <td>[{'name': 'Other economic management', 'code':...</td>
      <td>54,24</td>
      <td>0</td>
      <td>4700000</td>
      <td>http://www.worldbank.org/projects/P144674?lang=en</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 50 columns</p>
</div>



****
## JSON exercise

Using data in file 'data/world_bank_projects.json' and the techniques demonstrated above,
1. Find the 10 countries with most projects
2. Find the top 10 major project themes (using column 'mjtheme_namecode')
3. In 2. above you will notice that some entries have only the code and the name is missing. Create a dataframe with the missing names filled in.


```python
df= pd.read_json('world_bank_projects.json')
df
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
      <th>_id</th>
      <th>approvalfy</th>
      <th>board_approval_month</th>
      <th>boardapprovaldate</th>
      <th>borrower</th>
      <th>closingdate</th>
      <th>country_namecode</th>
      <th>countrycode</th>
      <th>countryname</th>
      <th>countryshortname</th>
      <th>...</th>
      <th>sectorcode</th>
      <th>source</th>
      <th>status</th>
      <th>supplementprojectflg</th>
      <th>theme1</th>
      <th>theme_namecode</th>
      <th>themecode</th>
      <th>totalamt</th>
      <th>totalcommamt</th>
      <th>url</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>{'$oid': '52b213b38594d8a2be17c780'}</td>
      <td>1999</td>
      <td>November</td>
      <td>2013-11-12T00:00:00Z</td>
      <td>FEDERAL DEMOCRATIC REPUBLIC OF ETHIOPIA</td>
      <td>2018-07-07T00:00:00Z</td>
      <td>Federal Democratic Republic of Ethiopia!$!ET</td>
      <td>ET</td>
      <td>Federal Democratic Republic of Ethiopia</td>
      <td>Ethiopia</td>
      <td>...</td>
      <td>ET,BS,ES,EP</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Education for all'}</td>
      <td>[{'code': '65', 'name': 'Education for all'}]</td>
      <td>65</td>
      <td>130000000</td>
      <td>130000000</td>
      <td>http://www.worldbank.org/projects/P129828/ethi...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>{'$oid': '52b213b38594d8a2be17c781'}</td>
      <td>2015</td>
      <td>November</td>
      <td>2013-11-04T00:00:00Z</td>
      <td>GOVERNMENT OF TUNISIA</td>
      <td>NaN</td>
      <td>Republic of Tunisia!$!TN</td>
      <td>TN</td>
      <td>Republic of Tunisia</td>
      <td>Tunisia</td>
      <td>...</td>
      <td>BZ,BS</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 30, 'Name': 'Other economic manage...</td>
      <td>[{'code': '24', 'name': 'Other economic manage...</td>
      <td>54,24</td>
      <td>0</td>
      <td>4700000</td>
      <td>http://www.worldbank.org/projects/P144674?lang=en</td>
    </tr>
    <tr>
      <th>2</th>
      <td>{'$oid': '52b213b38594d8a2be17c782'}</td>
      <td>2014</td>
      <td>November</td>
      <td>2013-11-01T00:00:00Z</td>
      <td>MINISTRY OF FINANCE AND ECONOMIC DEVEL</td>
      <td>NaN</td>
      <td>Tuvalu!$!TV</td>
      <td>TV</td>
      <td>Tuvalu</td>
      <td>Tuvalu</td>
      <td>...</td>
      <td>TI</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>Y</td>
      <td>{'Percent': 46, 'Name': 'Regional integration'}</td>
      <td>[{'code': '47', 'name': 'Regional integration'...</td>
      <td>52,81,25,47</td>
      <td>6060000</td>
      <td>6060000</td>
      <td>http://www.worldbank.org/projects/P145310?lang=en</td>
    </tr>
    <tr>
      <th>3</th>
      <td>{'$oid': '52b213b38594d8a2be17c783'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-31T00:00:00Z</td>
      <td>MIN. OF PLANNING AND INT'L COOPERATION</td>
      <td>NaN</td>
      <td>Republic of Yemen!$!RY</td>
      <td>RY</td>
      <td>Republic of Yemen</td>
      <td>Yemen, Republic of</td>
      <td>...</td>
      <td>JB</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 50, 'Name': 'Participation and civ...</td>
      <td>[{'code': '57', 'name': 'Participation and civ...</td>
      <td>59,57</td>
      <td>0</td>
      <td>1500000</td>
      <td>http://www.worldbank.org/projects/P144665?lang=en</td>
    </tr>
    <tr>
      <th>4</th>
      <td>{'$oid': '52b213b38594d8a2be17c784'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-31T00:00:00Z</td>
      <td>MINISTRY OF FINANCE</td>
      <td>2019-04-30T00:00:00Z</td>
      <td>Kingdom of Lesotho!$!LS</td>
      <td>LS</td>
      <td>Kingdom of Lesotho</td>
      <td>Lesotho</td>
      <td>...</td>
      <td>FH,YW,YZ</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 30, 'Name': 'Export development an...</td>
      <td>[{'code': '45', 'name': 'Export development an...</td>
      <td>41,45</td>
      <td>13100000</td>
      <td>13100000</td>
      <td>http://www.worldbank.org/projects/P144933/seco...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>{'$oid': '52b213b38594d8a2be17c785'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-31T00:00:00Z</td>
      <td>REPUBLIC OF KENYA</td>
      <td>NaN</td>
      <td>Republic of Kenya!$!KE</td>
      <td>KE</td>
      <td>Republic of Kenya</td>
      <td>Kenya</td>
      <td>...</td>
      <td>JB</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>Y</td>
      <td>{'Percent': 100, 'Name': 'Social safety nets'}</td>
      <td>[{'code': '54', 'name': 'Social safety nets'}]</td>
      <td>54</td>
      <td>10000000</td>
      <td>10000000</td>
      <td>http://www.worldbank.org/projects/P146161?lang=en</td>
    </tr>
    <tr>
      <th>6</th>
      <td>{'$oid': '52b213b38594d8a2be17c786'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-29T00:00:00Z</td>
      <td>GOVERNMENT OF INDIA</td>
      <td>2019-06-30T00:00:00Z</td>
      <td>Republic of India!$!IN</td>
      <td>IN</td>
      <td>Republic of India</td>
      <td>India</td>
      <td>...</td>
      <td>TI</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 20, 'Name': 'Administrative and ci...</td>
      <td>[{'code': '25', 'name': 'Administrative and ci...</td>
      <td>39,25</td>
      <td>500000000</td>
      <td>500000000</td>
      <td>http://www.worldbank.org/projects/P121185/firs...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>{'$oid': '52b213b38594d8a2be17c787'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-29T00:00:00Z</td>
      <td>PEOPLE'S REPUBLIC OF CHINA</td>
      <td>NaN</td>
      <td>People's Republic of China!$!CN</td>
      <td>CN</td>
      <td>People's Republic of China</td>
      <td>China</td>
      <td>...</td>
      <td>LR</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Climate change'}</td>
      <td>[{'code': '81', 'name': 'Climate change'}]</td>
      <td>81</td>
      <td>0</td>
      <td>27280000</td>
      <td>http://www.worldbank.org/projects/P127033/chin...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>{'$oid': '52b213b38594d8a2be17c788'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-29T00:00:00Z</td>
      <td>THE GOVERNMENT OF INDIA</td>
      <td>2018-12-31T00:00:00Z</td>
      <td>Republic of India!$!IN</td>
      <td>IN</td>
      <td>Republic of India</td>
      <td>India</td>
      <td>...</td>
      <td>TI</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 87, 'Name': 'Other rural developme...</td>
      <td>[{'code': '79', 'name': 'Other rural developme...</td>
      <td>79</td>
      <td>160000000</td>
      <td>160000000</td>
      <td>http://www.worldbank.org/projects/P130164/raja...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>{'$oid': '52b213b38594d8a2be17c789'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-29T00:00:00Z</td>
      <td>THE KINGDOM OF MOROCCO</td>
      <td>2014-12-31T00:00:00Z</td>
      <td>Kingdom of Morocco!$!MA</td>
      <td>MA</td>
      <td>Kingdom of Morocco</td>
      <td>Morocco</td>
      <td>...</td>
      <td>BM,BC,BZ</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 33, 'Name': 'Other accountability/...</td>
      <td>[{'code': '29', 'name': 'Other accountability/...</td>
      <td>27,30,29</td>
      <td>200000000</td>
      <td>200000000</td>
      <td>http://www.worldbank.org/projects/P130903?lang=en</td>
    </tr>
    <tr>
      <th>10</th>
      <td>{'$oid': '52b213b38594d8a2be17c78a'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-25T00:00:00Z</td>
      <td>GOVERNMENT OF SOUTH SUDAN</td>
      <td>NaN</td>
      <td>Republic of South Sudan!$!SS</td>
      <td>SS</td>
      <td>Republic of South Sudan</td>
      <td>South Sudan</td>
      <td>...</td>
      <td>AZ,JB,AH</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>Y</td>
      <td>{'Percent': 100, 'Name': 'Global food crisis r...</td>
      <td>[{'code': '91', 'name': 'Global food crisis re...</td>
      <td>91</td>
      <td>0</td>
      <td>7530000</td>
      <td>http://www.worldbank.org/projects/P145339?lang=en</td>
    </tr>
    <tr>
      <th>11</th>
      <td>{'$oid': '52b213b38594d8a2be17c78b'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-25T00:00:00Z</td>
      <td>NaN</td>
      <td>2017-12-31T00:00:00Z</td>
      <td>Republic of India!$!IN</td>
      <td>IN</td>
      <td>Republic of India</td>
      <td>India</td>
      <td>...</td>
      <td>JB,YC,WD,TI</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 60, 'Name': 'Rural services and in...</td>
      <td>[{'code': '78', 'name': 'Rural services and in...</td>
      <td>81,87,52,78</td>
      <td>250000000</td>
      <td>250000000</td>
      <td>http://www.worldbank.org/projects/P146653?lang=en</td>
    </tr>
    <tr>
      <th>12</th>
      <td>{'$oid': '52b213b38594d8a2be17c78c'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-24T00:00:00Z</td>
      <td>GOVERNMENT OF GHANA</td>
      <td>2019-06-30T00:00:00Z</td>
      <td>Republic of Ghana!$!GH</td>
      <td>GH</td>
      <td>Republic of Ghana</td>
      <td>Ghana</td>
      <td>...</td>
      <td>CZ</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 0, 'Name': ''}</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>97000000</td>
      <td>97000000</td>
      <td>http://www.worldbank.org/projects/P144140/gh-e...</td>
    </tr>
    <tr>
      <th>13</th>
      <td>{'$oid': '52b213b38594d8a2be17c78d'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-22T00:00:00Z</td>
      <td>GOVERNMENT OF TIMOR LESTE</td>
      <td>NaN</td>
      <td>Democratic Republic of Timor-Leste!$!TP</td>
      <td>TP</td>
      <td>Democratic Republic of Timor-Leste</td>
      <td>Timor-Leste</td>
      <td>...</td>
      <td>BV,TI</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>Y</td>
      <td>{'Percent': 20, 'Name': 'Regional integration'}</td>
      <td>[{'code': '47', 'name': 'Regional integration'...</td>
      <td>78,81,47</td>
      <td>40000000</td>
      <td>40000000</td>
      <td>http://www.worldbank.org/projects/P130975/timo...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>{'$oid': '52b213b38594d8a2be17c78e'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-22T00:00:00Z</td>
      <td>GOVERNMENT OF JORDAN</td>
      <td>NaN</td>
      <td>Hashemite Kingdom of Jordan!$!JO</td>
      <td>JO</td>
      <td>Hashemite Kingdom of Jordan</td>
      <td>Jordan</td>
      <td>...</td>
      <td>JB</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 50, 'Name': 'Social safety nets'}</td>
      <td>[{'code': '54', 'name': 'Social safety nets'},...</td>
      <td>53,56,54</td>
      <td>0</td>
      <td>9500000</td>
      <td>http://www.worldbank.org/projects/P144832?lang=en</td>
    </tr>
    <tr>
      <th>15</th>
      <td>{'$oid': '52b213b38594d8a2be17c78f'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-17T00:00:00Z</td>
      <td>MINISTRY OF FINANCE</td>
      <td>2019-04-30T00:00:00Z</td>
      <td>Samoa!$!WS</td>
      <td>WS</td>
      <td>Samoa</td>
      <td>Samoa</td>
      <td>...</td>
      <td>TI</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 60, 'Name': 'Rural services and in...</td>
      <td>[{'code': '78', 'name': 'Rural services and in...</td>
      <td>49,81,78</td>
      <td>20000000</td>
      <td>20000000</td>
      <td>http://www.worldbank.org/projects/P145545?lang=en</td>
    </tr>
    <tr>
      <th>16</th>
      <td>{'$oid': '52b213b38594d8a2be17c790'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-17T00:00:00Z</td>
      <td>MINISTRY OF FINANCE</td>
      <td>2015-12-31T00:00:00Z</td>
      <td>Samoa!$!WS</td>
      <td>WS</td>
      <td>Samoa</td>
      <td>Samoa</td>
      <td>...</td>
      <td>AZ,AJ,AH</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Other rural developm...</td>
      <td>[{'code': '79', 'name': 'Other rural developme...</td>
      <td>79</td>
      <td>5000000</td>
      <td>5000000</td>
      <td>http://www.worldbank.org/projects/P145938?lang=en</td>
    </tr>
    <tr>
      <th>17</th>
      <td>{'$oid': '52b213b38594d8a2be17c791'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-16T00:00:00Z</td>
      <td>MINISTRY OF FINANCE AND BUDGET (MFB)</td>
      <td>NaN</td>
      <td>Republic of Madagascar!$!MG</td>
      <td>MG</td>
      <td>Republic of Madagascar</td>
      <td>Madagascar</td>
      <td>...</td>
      <td>EP</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Education for all'}</td>
      <td>[{'code': '65', 'name': 'Education for all'}]</td>
      <td>65</td>
      <td>0</td>
      <td>85400000</td>
      <td>http://www.worldbank.org/projects/P132616?lang=en</td>
    </tr>
    <tr>
      <th>18</th>
      <td>{'$oid': '52b213b38594d8a2be17c792'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-16T00:00:00Z</td>
      <td>ROYAL GOVERNMENT OF CAMBODIA</td>
      <td>NaN</td>
      <td>Kingdom of Cambodia!$!KH</td>
      <td>KH</td>
      <td>Kingdom of Cambodia</td>
      <td>Cambodia</td>
      <td>...</td>
      <td>BK,JB,BH,BC,JA</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>Y</td>
      <td>{'Percent': 17, 'Name': 'Child health'}</td>
      <td>[{'code': '63', 'name': 'Child health'}, {'cod...</td>
      <td>69,57,25,67,63</td>
      <td>0</td>
      <td>13450000</td>
      <td>http://www.worldbank.org/projects/P146271?lang=en</td>
    </tr>
    <tr>
      <th>19</th>
      <td>{'$oid': '52b213b38594d8a2be17c793'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-10T00:00:00Z</td>
      <td>MINISTRY OF FINANCE</td>
      <td>NaN</td>
      <td>Kingdom of Morocco!$!MA</td>
      <td>MA</td>
      <td>Kingdom of Morocco</td>
      <td>Morocco</td>
      <td>...</td>
      <td>BH,BC,BZ</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 40, 'Name': 'Public expenditure, f...</td>
      <td>[{'code': '27', 'name': 'Public expenditure, f...</td>
      <td>25,26,27</td>
      <td>0</td>
      <td>4350000</td>
      <td>http://www.worldbank.org/projects/P143979?lang=en</td>
    </tr>
    <tr>
      <th>20</th>
      <td>{'$oid': '52b213b38594d8a2be17c794'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-09T00:00:00Z</td>
      <td>AGA KHAN DEVELOPMENT NETWORK (AKDN)</td>
      <td>NaN</td>
      <td>Kyrgyz Republic!$!KG</td>
      <td>KG</td>
      <td>Kyrgyz Republic</td>
      <td>Kyrgyz Republic</td>
      <td>...</td>
      <td>JB</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 50, 'Name': 'Conflict prevention a...</td>
      <td>[{'code': '58', 'name': 'Conflict prevention a...</td>
      <td>57,58</td>
      <td>0</td>
      <td>2000000</td>
      <td>http://www.worldbank.org/projects/P132577?lang=en</td>
    </tr>
    <tr>
      <th>21</th>
      <td>{'$oid': '52b213b38594d8a2be17c795'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-07T00:00:00Z</td>
      <td>NEPAL</td>
      <td>NaN</td>
      <td>Nepal!$!NP</td>
      <td>NP</td>
      <td>Nepal</td>
      <td>Nepal</td>
      <td>...</td>
      <td>BH,YW,JB</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 30, 'Name': 'Urban services and ho...</td>
      <td>[{'code': '71', 'name': 'Urban services and ho...</td>
      <td>57,71</td>
      <td>0</td>
      <td>2750000</td>
      <td>http://www.worldbank.org/projects/P145359?lang=en</td>
    </tr>
    <tr>
      <th>22</th>
      <td>{'$oid': '52b213b38594d8a2be17c796'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-07T00:00:00Z</td>
      <td>MINISTRY OF PLANNING AND INTERNATIONAL C</td>
      <td>NaN</td>
      <td>Hashemite Kingdom of Jordan!$!JO</td>
      <td>JO</td>
      <td>Hashemite Kingdom of Jordan</td>
      <td>Jordan</td>
      <td>...</td>
      <td>WC,BS,BH,TZ,WB</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 25, 'Name': 'Other social developm...</td>
      <td>[{'code': '62', 'name': 'Other social developm...</td>
      <td>58,62</td>
      <td>0</td>
      <td>50000000</td>
      <td>http://www.worldbank.org/projects/P147689?lang=en</td>
    </tr>
    <tr>
      <th>23</th>
      <td>{'$oid': '52b213b38594d8a2be17c797'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-03T00:00:00Z</td>
      <td>REPUBLIC OF TAJIKISTAN</td>
      <td>NaN</td>
      <td>Republic of Tajikistan!$!TJ</td>
      <td>TJ</td>
      <td>Republic of Tajikistan</td>
      <td>Tajikistan</td>
      <td>...</td>
      <td>JA</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 60, 'Name': 'Nutrition and food se...</td>
      <td>[{'code': '68', 'name': 'Nutrition and food se...</td>
      <td>63,68</td>
      <td>0</td>
      <td>2800000</td>
      <td>http://www.worldbank.org/projects/P146109?lang=en</td>
    </tr>
    <tr>
      <th>24</th>
      <td>{'$oid': '52b213b38594d8a2be17c798'}</td>
      <td>2014</td>
      <td>September</td>
      <td>2013-09-30T00:00:00Z</td>
      <td>REPUBLIC OF AZERBAIJAN</td>
      <td>2018-12-31T00:00:00Z</td>
      <td>Republic of Azerbaijan!$!AZ</td>
      <td>AZ</td>
      <td>Republic of Azerbaijan</td>
      <td>Azerbaijan</td>
      <td>...</td>
      <td>AB,AZ,YA</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 30, 'Name': 'Rural markets'}</td>
      <td>[{'code': '75', 'name': 'Rural markets'}, {'co...</td>
      <td>56,78,76,75</td>
      <td>34500000</td>
      <td>34500000</td>
      <td>http://www.worldbank.org/projects/P122812/thir...</td>
    </tr>
    <tr>
      <th>25</th>
      <td>{'$oid': '52b213b38594d8a2be17c799'}</td>
      <td>2014</td>
      <td>September</td>
      <td>2013-09-30T00:00:00Z</td>
      <td>UNIVERSITY OF QUEENSLAND</td>
      <td>NaN</td>
      <td>East Asia and Pacific!$!4E</td>
      <td>4E</td>
      <td>East Asia and Pacific</td>
      <td>East Asia and Pacific</td>
      <td>...</td>
      <td>AB,AZ</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 40, 'Name': 'Other environment and...</td>
      <td>[{'code': '86', 'name': 'Other environment and...</td>
      <td>80,81,86</td>
      <td>0</td>
      <td>4500000</td>
      <td>http://www.worldbank.org/projects/P123933/capt...</td>
    </tr>
    <tr>
      <th>26</th>
      <td>{'$oid': '52b213b38594d8a2be17c79a'}</td>
      <td>2014</td>
      <td>September</td>
      <td>2013-09-30T00:00:00Z</td>
      <td>LAO PEOPLES DEMOCRATIC REPUBLIC</td>
      <td>2014-03-31T00:00:00Z</td>
      <td>Lao People's Democratic Republic!$!LA</td>
      <td>LA</td>
      <td>Lao People's Democratic Republic</td>
      <td>Lao People's Democratic Republic</td>
      <td>...</td>
      <td>LG,FB,EZ,YZ,BC</td>
      <td>IBRD</td>
      <td>Closed</td>
      <td>N</td>
      <td>{'Percent': 14, 'Name': 'Regulation and compet...</td>
      <td>[{'code': '40', 'name': 'Regulation and compet...</td>
      <td>67,27,49,40</td>
      <td>20000000</td>
      <td>20000000</td>
      <td>http://www.worldbank.org/projects/P143025/lao-...</td>
    </tr>
    <tr>
      <th>27</th>
      <td>{'$oid': '52b213b38594d8a2be17c79b'}</td>
      <td>2014</td>
      <td>September</td>
      <td>2013-09-30T00:00:00Z</td>
      <td>PACIFIC AVIATION SECURITY OFFICE</td>
      <td>2018-12-31T00:00:00Z</td>
      <td>Pacific Islands!$!4P</td>
      <td>4P</td>
      <td>Pacific Islands</td>
      <td>Pacific Islands</td>
      <td>...</td>
      <td>BV,TV</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 5, 'Name': 'Climate change'}</td>
      <td>[{'code': '81', 'name': 'Climate change'}, {'c...</td>
      <td>52,47,25,81</td>
      <td>2150000</td>
      <td>2150000</td>
      <td>http://www.worldbank.org/projects/P145057/paci...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>{'$oid': '52b213b38594d8a2be17c79c'}</td>
      <td>2014</td>
      <td>September</td>
      <td>2013-09-30T00:00:00Z</td>
      <td>SOLOMON ISLANDS GOVERNMENT</td>
      <td>NaN</td>
      <td>Solomon Islands!$!SB</td>
      <td>SB</td>
      <td>Solomon Islands</td>
      <td>Solomon Islands</td>
      <td>...</td>
      <td>BZ,AZ</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>Y</td>
      <td>{'Percent': 30, 'Name': 'Rural policies and in...</td>
      <td>[{'code': '77', 'name': 'Rural policies and in...</td>
      <td>57,78,77</td>
      <td>3000000</td>
      <td>3000000</td>
      <td>http://www.worldbank.org/projects/P146021?lang=en</td>
    </tr>
    <tr>
      <th>29</th>
      <td>{'$oid': '52b213b38594d8a2be17c79d'}</td>
      <td>2014</td>
      <td>September</td>
      <td>2013-09-27T00:00:00Z</td>
      <td>GOVERNMENT OF MOZAMBIQUE</td>
      <td>NaN</td>
      <td>Republic of Mozambique!$!MZ</td>
      <td>MZ</td>
      <td>Republic of Mozambique</td>
      <td>Mozambique</td>
      <td>...</td>
      <td>JB,BW,WZ,WD</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>Y</td>
      <td>{'Percent': 4, 'Name': 'Other social developme...</td>
      <td>[{'code': '62', 'name': 'Other social developm...</td>
      <td>85,62</td>
      <td>32000000</td>
      <td>32000000</td>
      <td>http://www.worldbank.org/projects/P146098?lang=en</td>
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
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>470</th>
      <td>{'$oid': '52b213b38594d8a2be17c956'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-20T00:00:00Z</td>
      <td>GOVERNMENT OF LIBERIA</td>
      <td>NaN</td>
      <td>Republic of Liberia!$!LR</td>
      <td>LR</td>
      <td>Republic of Liberia</td>
      <td>Liberia</td>
      <td>...</td>
      <td>BV,TI</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>Y</td>
      <td>{'Percent': 40, 'Name': 'Trade facilitation an...</td>
      <td>[{'code': '49', 'name': 'Trade facilitation an...</td>
      <td>78,49</td>
      <td>50000000</td>
      <td>50000000</td>
      <td>http://www.worldbank.org/projects/P129654/libe...</td>
    </tr>
    <tr>
      <th>471</th>
      <td>{'$oid': '52b213b38594d8a2be17c957'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-20T00:00:00Z</td>
      <td>GOVERNMENT OF BANGLADESH</td>
      <td>2018-12-31T00:00:00Z</td>
      <td>People's Republic of Bangladesh!$!BD</td>
      <td>BD</td>
      <td>People's Republic of Bangladesh</td>
      <td>Bangladesh</td>
      <td>...</td>
      <td>BU,LA,LR</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 45, 'Name': 'Rural services and in...</td>
      <td>[{'code': '78', 'name': 'Rural services and in...</td>
      <td>59,81,57,78</td>
      <td>155000000</td>
      <td>155000000</td>
      <td>http://www.worldbank.org/projects/P131263/rura...</td>
    </tr>
    <tr>
      <th>472</th>
      <td>{'$oid': '52b213b38594d8a2be17c958'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-13T00:00:00Z</td>
      <td>MINISTRY OF NATURE PROTECTION</td>
      <td>2014-09-30T00:00:00Z</td>
      <td>Republic of Armenia!$!AM</td>
      <td>AM</td>
      <td>Republic of Armenia</td>
      <td>Armenia</td>
      <td>...</td>
      <td>BC</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Other environment an...</td>
      <td>[{'code': '86', 'name': 'Other environment and...</td>
      <td>86</td>
      <td>0</td>
      <td>150000</td>
      <td>http://www.worldbank.org/projects/P131631/repo...</td>
    </tr>
    <tr>
      <th>473</th>
      <td>{'$oid': '52b213b38594d8a2be17c959'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-13T00:00:00Z</td>
      <td>MINISTRY OF ENVIRONMENT, FORESTS, WATER</td>
      <td>NaN</td>
      <td>Republic of Albania!$!AL</td>
      <td>AL</td>
      <td>Republic of Albania</td>
      <td>Albania</td>
      <td>...</td>
      <td>BC</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Other environment an...</td>
      <td>[{'code': '86', 'name': 'Other environment and...</td>
      <td>86</td>
      <td>0</td>
      <td>150000</td>
      <td>http://www.worldbank.org/projects/P132679/land...</td>
    </tr>
    <tr>
      <th>474</th>
      <td>{'$oid': '52b213b38594d8a2be17c95a'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-11T00:00:00Z</td>
      <td>GOVERNMENT OF PAKISTAN</td>
      <td>2017-06-30T00:00:00Z</td>
      <td>Islamic Republic of Pakistan!$!PK</td>
      <td>PK</td>
      <td>Islamic Republic of Pakistan</td>
      <td>Pakistan</td>
      <td>...</td>
      <td>BM,BH</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 34, 'Name': 'Municipal finance'}</td>
      <td>[{'code': '72', 'name': 'Municipal finance'}, ...</td>
      <td>73,72</td>
      <td>150000000</td>
      <td>150000000</td>
      <td>http://www.worldbank.org/projects/P112901/pk-p...</td>
    </tr>
    <tr>
      <th>475</th>
      <td>{'$oid': '52b213b38594d8a2be17c95b'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-11T00:00:00Z</td>
      <td>GOVERNMENT OF INDONESIA</td>
      <td>2018-03-31T00:00:00Z</td>
      <td>Republic of Indonesia!$!ID</td>
      <td>ID</td>
      <td>Republic of Indonesia</td>
      <td>Indonesia</td>
      <td>...</td>
      <td>BO,BH,LZ,TZ,WZ</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 25, 'Name': 'Infrastructure servic...</td>
      <td>[{'code': '39', 'name': 'Infrastructure servic...</td>
      <td>72,39</td>
      <td>29600000</td>
      <td>29600000</td>
      <td>http://www.worldbank.org/projects/P118916/infr...</td>
    </tr>
    <tr>
      <th>476</th>
      <td>{'$oid': '52b213b38594d8a2be17c95c'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-11T00:00:00Z</td>
      <td>SOCIALIST REPUBLIC OF VIETNAM</td>
      <td>2018-12-31T00:00:00Z</td>
      <td>Socialist Republic of Vietnam!$!VN</td>
      <td>VN</td>
      <td>Socialist Republic of Vietnam</td>
      <td>Vietnam</td>
      <td>...</td>
      <td>BU,LT,LA</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Rural services and i...</td>
      <td>[{'code': '78', 'name': 'Rural services and in...</td>
      <td>78</td>
      <td>448900000</td>
      <td>448900000</td>
      <td>http://www.worldbank.org/projects/P125996/dist...</td>
    </tr>
    <tr>
      <th>477</th>
      <td>{'$oid': '52b213b38594d8a2be17c95d'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-11T00:00:00Z</td>
      <td>REPUBLIC OF UZBEKISTAN</td>
      <td>NaN</td>
      <td>Republic of Uzbekistan!$!UZ</td>
      <td>UZ</td>
      <td>Republic of Uzbekistan</td>
      <td>Uzbekistan</td>
      <td>...</td>
      <td>FH</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>Y</td>
      <td>{'Percent': 40, 'Name': 'Micro, Small and Medi...</td>
      <td>[{'code': '41', 'name': 'Micro, Small and Medi...</td>
      <td>75,41</td>
      <td>40000000</td>
      <td>40000000</td>
      <td>http://www.worldbank.org/projects/P126962/addi...</td>
    </tr>
    <tr>
      <th>478</th>
      <td>{'$oid': '52b213b38594d8a2be17c95e'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-11T00:00:00Z</td>
      <td>ISLAMIC REPUBLIC OF PAKISTAN</td>
      <td>NaN</td>
      <td>Islamic Republic of Pakistan!$!PK</td>
      <td>PK</td>
      <td>Islamic Republic of Pakistan</td>
      <td>Pakistan</td>
      <td>...</td>
      <td>BH</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>Y</td>
      <td>{'Percent': 10, 'Name': 'Administrative and ci...</td>
      <td>[{'code': '25', 'name': 'Administrative and ci...</td>
      <td>83,36,25</td>
      <td>70000000</td>
      <td>70000000</td>
      <td>http://www.worldbank.org/projects/P131266/punj...</td>
    </tr>
    <tr>
      <th>479</th>
      <td>{'$oid': '52b213b38594d8a2be17c95f'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-10T00:00:00Z</td>
      <td>UT'Z CHE</td>
      <td>2016-05-07T00:00:00Z</td>
      <td>Republic of Guatemala!$!GT</td>
      <td>GT</td>
      <td>Republic of Guatemala</td>
      <td>Guatemala</td>
      <td>...</td>
      <td>AZ</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Other social develop...</td>
      <td>[{'code': '62', 'name': 'Other social developm...</td>
      <td>62</td>
      <td>0</td>
      <td>2510000</td>
      <td>http://www.worldbank.org/projects/P130412/stre...</td>
    </tr>
    <tr>
      <th>480</th>
      <td>{'$oid': '52b213b38594d8a2be17c960'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-10T00:00:00Z</td>
      <td>GOVERNMENT OF ZAMBIA</td>
      <td>2014-12-31T00:00:00Z</td>
      <td>Republic of Zambia!$!ZM</td>
      <td>ZM</td>
      <td>Republic of Zambia</td>
      <td>Zambia</td>
      <td>...</td>
      <td>LS</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Other public sector ...</td>
      <td>[{'code': '30', 'name': 'Other public sector g...</td>
      <td>30</td>
      <td>0</td>
      <td>350000</td>
      <td>http://www.worldbank.org/projects/P131881/zamb...</td>
    </tr>
    <tr>
      <th>481</th>
      <td>{'$oid': '52b213b38594d8a2be17c961'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-06T00:00:00Z</td>
      <td>GOVERNMENT OF INDIA</td>
      <td>2015-12-31T00:00:00Z</td>
      <td>Republic of India!$!IN</td>
      <td>IN</td>
      <td>Republic of India</td>
      <td>India</td>
      <td>...</td>
      <td>BC,EC,BQ,BH</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 23, 'Name': 'Child health'}</td>
      <td>[{'code': '63', 'name': 'Child health'}, {'cod...</td>
      <td>68,59,57,63</td>
      <td>106000000</td>
      <td>106000000</td>
      <td>http://www.worldbank.org/projects/P121731/icds...</td>
    </tr>
    <tr>
      <th>482</th>
      <td>{'$oid': '52b213b38594d8a2be17c962'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-06T00:00:00Z</td>
      <td>GOVERNMENT OF INDIA</td>
      <td>2018-12-31T00:00:00Z</td>
      <td>Republic of India!$!IN</td>
      <td>IN</td>
      <td>Republic of India</td>
      <td>India</td>
      <td>...</td>
      <td>AI,YA,AH,BL,AB</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 10, 'Name': 'Rural services and in...</td>
      <td>[{'code': '78', 'name': 'Rural services and in...</td>
      <td>79,85,86,78</td>
      <td>60000000</td>
      <td>60000000</td>
      <td>http://www.worldbank.org/projects/P122486/karn...</td>
    </tr>
    <tr>
      <th>483</th>
      <td>{'$oid': '52b213b38594d8a2be17c963'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-06T00:00:00Z</td>
      <td>GOVERNMENT OF INDIA</td>
      <td>2013-09-30T00:00:00Z</td>
      <td>Republic of India!$!IN</td>
      <td>IN</td>
      <td>Republic of India</td>
      <td>India</td>
      <td>...</td>
      <td>CZ,AH,LA,AI,LH</td>
      <td>IBRD</td>
      <td>Closed</td>
      <td>N</td>
      <td>{'Percent': 19, 'Name': 'Pollution management ...</td>
      <td>[{'code': '84', 'name': 'Pollution management ...</td>
      <td>82,78,81,84</td>
      <td>100000000</td>
      <td>100000000</td>
      <td>http://www.worldbank.org/projects/P124041/hima...</td>
    </tr>
    <tr>
      <th>484</th>
      <td>{'$oid': '52b213b38594d8a2be17c964'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-06T00:00:00Z</td>
      <td>ILO, MINLAND &amp; CFSI &amp; BANK</td>
      <td>2015-12-31T00:00:00Z</td>
      <td>Republic of the Philippines!$!PH</td>
      <td>PH</td>
      <td>Republic of the Philippines</td>
      <td>Philippines</td>
      <td>...</td>
      <td>EV,FH,BZ,JB</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>Y</td>
      <td>{'Percent': 9, 'Name': 'Rural non-farm income ...</td>
      <td>[{'code': '76', 'name': 'Rural non-farm income...</td>
      <td>78,58,41,76</td>
      <td>0</td>
      <td>5570000</td>
      <td>http://www.worldbank.org/projects/P132238/mult...</td>
    </tr>
    <tr>
      <th>485</th>
      <td>{'$oid': '52b213b38594d8a2be17c965'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-05T00:00:00Z</td>
      <td>GOVERNMENT OF MONGOLIA</td>
      <td>2013-12-31T00:00:00Z</td>
      <td>Mongolia!$!MN</td>
      <td>MN</td>
      <td>Mongolia</td>
      <td>Mongolia</td>
      <td>...</td>
      <td>BZ,JA,AJ</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Other communicable d...</td>
      <td>[{'code': '64', 'name': 'Other communicable di...</td>
      <td>64</td>
      <td>0</td>
      <td>2900000</td>
      <td>http://www.worldbank.org/projects/P131204/capa...</td>
    </tr>
    <tr>
      <th>486</th>
      <td>{'$oid': '52b213b38594d8a2be17c966'}</td>
      <td>2013</td>
      <td>September</td>
      <td>2012-09-01T00:00:00Z</td>
      <td>GOVERNMENT OF LEBANON &amp; JORDAN</td>
      <td>2015-01-31T00:00:00Z</td>
      <td>Middle East and North Africa!$!5M</td>
      <td>5M</td>
      <td>Middle East and North Africa</td>
      <td>Middle East and North Africa</td>
      <td>...</td>
      <td>BZ,BS,BQ,BN</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 25, 'Name': 'Other public sector g...</td>
      <td>[{'code': '30', 'name': 'Other public sector g...</td>
      <td>54,55,56,30</td>
      <td>0</td>
      <td>2400000</td>
      <td>http://www.worldbank.org/projects/P132097/5m-d...</td>
    </tr>
    <tr>
      <th>487</th>
      <td>{'$oid': '52b213b38594d8a2be17c967'}</td>
      <td>2013</td>
      <td>August</td>
      <td>2012-08-30T00:00:00Z</td>
      <td>UNITED MEXICAN STATES</td>
      <td>2017-08-31T00:00:00Z</td>
      <td>United Mexican States!$!MX</td>
      <td>MX</td>
      <td>United Mexican States</td>
      <td>Mexico</td>
      <td>...</td>
      <td>YA,BL,AB</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 20, 'Name': 'Biodiversity'}</td>
      <td>[{'code': '80', 'name': 'Biodiversity'}, {'cod...</td>
      <td>82,79,77,80</td>
      <td>0</td>
      <td>11690000</td>
      <td>http://www.worldbank.org/projects/P121116/sust...</td>
    </tr>
    <tr>
      <th>488</th>
      <td>{'$oid': '52b213b38594d8a2be17c968'}</td>
      <td>2013</td>
      <td>August</td>
      <td>2012-08-30T00:00:00Z</td>
      <td>THE STATE OF RIO DE JANEIRO</td>
      <td>2014-01-31T00:00:00Z</td>
      <td>Federative Republic of Brazil!$!BR</td>
      <td>BR</td>
      <td>Federative Republic of Brazil</td>
      <td>Brazil</td>
      <td>...</td>
      <td>JA,EZ,BH</td>
      <td>IBRD</td>
      <td>Closed</td>
      <td>N</td>
      <td>{'Percent': 20, 'Name': 'Health system perform...</td>
      <td>[{'code': '67', 'name': 'Health system perform...</td>
      <td>65,28,27,67</td>
      <td>300000000</td>
      <td>300000000</td>
      <td>http://www.worldbank.org/projects/P126465/rio-...</td>
    </tr>
    <tr>
      <th>489</th>
      <td>{'$oid': '52b213b38594d8a2be17c969'}</td>
      <td>2013</td>
      <td>August</td>
      <td>2012-08-30T00:00:00Z</td>
      <td>UN-HABITAT</td>
      <td>2015-06-30T00:00:00Z</td>
      <td>The Independent State of Papua New Guine!$!PG</td>
      <td>PG</td>
      <td>The Independent State of Papua New Guine</td>
      <td>Papua New Guinea</td>
      <td>...</td>
      <td>BW</td>
      <td>IBRD</td>
      <td>Closed</td>
      <td>N</td>
      <td>{'Percent': 50, 'Name': 'Urban services and ho...</td>
      <td>[{'code': '71', 'name': 'Urban services and ho...</td>
      <td>73,55,52,71</td>
      <td>0</td>
      <td>350000</td>
      <td>http://www.worldbank.org/projects/P128763/papu...</td>
    </tr>
    <tr>
      <th>490</th>
      <td>{'$oid': '52b213b38594d8a2be17c96a'}</td>
      <td>2013</td>
      <td>August</td>
      <td>2012-08-29T00:00:00Z</td>
      <td>GOVERNMENT OF NEPAL</td>
      <td>2014-06-30T00:00:00Z</td>
      <td>Nepal!$!NP</td>
      <td>NP</td>
      <td>Nepal</td>
      <td>Nepal</td>
      <td>...</td>
      <td>BZ</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 80, 'Name': 'Public expenditure, f...</td>
      <td>[{'code': '27', 'name': 'Public expenditure, f...</td>
      <td>29,27</td>
      <td>0</td>
      <td>800000</td>
      <td>http://www.worldbank.org/projects/P131860/stre...</td>
    </tr>
    <tr>
      <th>491</th>
      <td>{'$oid': '52b213b38594d8a2be17c96b'}</td>
      <td>2013</td>
      <td>August</td>
      <td>2012-08-24T00:00:00Z</td>
      <td>PALESTINIAN WATER AUTHORITY</td>
      <td>2014-03-31T00:00:00Z</td>
      <td>West Bank and Gaza!$!GZ</td>
      <td>GZ</td>
      <td>West Bank and Gaza</td>
      <td>West Bank and Gaza</td>
      <td>...</td>
      <td>WC,WA</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Rural services and i...</td>
      <td>[{'code': '78', 'name': 'Rural services and in...</td>
      <td>78</td>
      <td>0</td>
      <td>3650000</td>
      <td>http://www.worldbank.org/projects/P123322/wate...</td>
    </tr>
    <tr>
      <th>492</th>
      <td>{'$oid': '52b213b38594d8a2be17c96c'}</td>
      <td>2013</td>
      <td>August</td>
      <td>2012-08-21T00:00:00Z</td>
      <td>GOVERNMENT OF PAKISTAN</td>
      <td>2015-06-30T00:00:00Z</td>
      <td>Islamic Republic of Pakistan!$!PK</td>
      <td>PK</td>
      <td>Islamic Republic of Pakistan</td>
      <td>Pakistan</td>
      <td>...</td>
      <td>EP</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 70, 'Name': 'Education for all'}</td>
      <td>[{'code': '65', 'name': 'Education for all'}, ...</td>
      <td>59,65</td>
      <td>0</td>
      <td>10000000</td>
      <td>http://www.worldbank.org/projects/P128096/paki...</td>
    </tr>
    <tr>
      <th>493</th>
      <td>{'$oid': '52b213b38594d8a2be17c96d'}</td>
      <td>2013</td>
      <td>August</td>
      <td>2012-08-21T00:00:00Z</td>
      <td>GOVERNMENT OF BANGLADESH</td>
      <td>2015-04-30T00:00:00Z</td>
      <td>People's Republic of Bangladesh!$!BD</td>
      <td>BD</td>
      <td>People's Republic of Bangladesh</td>
      <td>Bangladesh</td>
      <td>...</td>
      <td>BC</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Other environment an...</td>
      <td>[{'code': '86', 'name': 'Other environment and...</td>
      <td>86</td>
      <td>0</td>
      <td>150000</td>
      <td>http://www.worldbank.org/projects/P132138/revi...</td>
    </tr>
    <tr>
      <th>494</th>
      <td>{'$oid': '52b213b38594d8a2be17c96e'}</td>
      <td>2013</td>
      <td>August</td>
      <td>2012-08-17T00:00:00Z</td>
      <td>MINISTRY OF EDUCATION</td>
      <td>2014-06-30T00:00:00Z</td>
      <td>Nepal!$!NP</td>
      <td>NP</td>
      <td>Nepal</td>
      <td>Nepal</td>
      <td>...</td>
      <td>EZ</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Natural disaster man...</td>
      <td>[{'code': '52', 'name': 'Natural disaster mana...</td>
      <td>52</td>
      <td>0</td>
      <td>1510000</td>
      <td>http://www.worldbank.org/projects/P129177/nepa...</td>
    </tr>
    <tr>
      <th>495</th>
      <td>{'$oid': '52b213b38594d8a2be17c96f'}</td>
      <td>2013</td>
      <td>August</td>
      <td>2012-08-10T00:00:00Z</td>
      <td>THE COMPETITIVENESS COMPANY</td>
      <td>2013-08-31T00:00:00Z</td>
      <td>Jamaica!$!JM</td>
      <td>JM</td>
      <td>Jamaica</td>
      <td>Jamaica</td>
      <td>...</td>
      <td>EV,AZ</td>
      <td>IBRD</td>
      <td>Closed</td>
      <td>N</td>
      <td>{'Percent': 50, 'Name': 'Regulation and compet...</td>
      <td>[{'code': '40', 'name': 'Regulation and compet...</td>
      <td>62,40</td>
      <td>0</td>
      <td>50000</td>
      <td>http://www.worldbank.org/projects/P127299/tech...</td>
    </tr>
    <tr>
      <th>496</th>
      <td>{'$oid': '52b213b38594d8a2be17c970'}</td>
      <td>2013</td>
      <td>August</td>
      <td>2012-08-09T00:00:00Z</td>
      <td>LAO PEOPLES DEMOCRATIC REPUBLIC</td>
      <td>2012-12-31T00:00:00Z</td>
      <td>Lao People's Democratic Republic!$!LA</td>
      <td>LA</td>
      <td>Lao People's Democratic Republic</td>
      <td>Lao People's Democratic Republic</td>
      <td>...</td>
      <td>YZ,JA,EZ,FZ,BC</td>
      <td>IBRD</td>
      <td>Closed</td>
      <td>N</td>
      <td>{'Percent': 14, 'Name': 'Child health'}</td>
      <td>[{'code': '63', 'name': 'Child health'}, {'cod...</td>
      <td>65,27,49,63</td>
      <td>20000000</td>
      <td>20000000</td>
      <td>http://www.worldbank.org/projects/P125298/lao-...</td>
    </tr>
    <tr>
      <th>497</th>
      <td>{'$oid': '52b213b38594d8a2be17c971'}</td>
      <td>2013</td>
      <td>August</td>
      <td>2012-08-03T00:00:00Z</td>
      <td>GOVERNMENT OF THE REPUBLIC OF GUINEA</td>
      <td>2014-12-31T00:00:00Z</td>
      <td>Republic of Guinea!$!GN</td>
      <td>GN</td>
      <td>Republic of Guinea</td>
      <td>Guinea</td>
      <td>...</td>
      <td>AB,AH,AI</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Global food crisis r...</td>
      <td>[{'code': '91', 'name': 'Global food crisis re...</td>
      <td>91</td>
      <td>0</td>
      <td>20000000</td>
      <td>http://www.worldbank.org/projects/P128309/seco...</td>
    </tr>
    <tr>
      <th>498</th>
      <td>{'$oid': '52b213b38594d8a2be17c972'}</td>
      <td>2013</td>
      <td>August</td>
      <td>2012-08-02T00:00:00Z</td>
      <td>REPUBLIC OF INDONESIA</td>
      <td>2017-09-30T00:00:00Z</td>
      <td>Republic of Indonesia!$!ID</td>
      <td>ID</td>
      <td>Republic of Indonesia</td>
      <td>Indonesia</td>
      <td>...</td>
      <td>YA,BL,AB</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 85, 'Name': 'Rural services and in...</td>
      <td>[{'code': '78', 'name': 'Rural services and in...</td>
      <td>77,91,78</td>
      <td>80000000</td>
      <td>80000000</td>
      <td>http://www.worldbank.org/projects/P117243/sust...</td>
    </tr>
    <tr>
      <th>499</th>
      <td>{'$oid': '52b213b38594d8a2be17c973'}</td>
      <td>2013</td>
      <td>August</td>
      <td>2012-08-02T00:00:00Z</td>
      <td>GOVERMENT OF KENYA</td>
      <td>2018-12-31T00:00:00Z</td>
      <td>Republic of Kenya!$!KE</td>
      <td>KE</td>
      <td>Republic of Kenya</td>
      <td>Kenya</td>
      <td>...</td>
      <td>BV,TC</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 1, 'Name': 'Municipal governance a...</td>
      <td>[{'code': '73', 'name': 'Municipal governance ...</td>
      <td>39,49,88,73</td>
      <td>300000000</td>
      <td>300000000</td>
      <td>http://www.worldbank.org/projects/P126321/keny...</td>
    </tr>
  </tbody>
</table>
<p>500 rows × 50 columns</p>
</div>




```python
print(df.shape)


```

    (500, 50)
    


```python
print(df.info())

```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 500 entries, 0 to 499
    Data columns (total 50 columns):
    _id                         500 non-null object
    approvalfy                  500 non-null int64
    board_approval_month        500 non-null object
    boardapprovaldate           500 non-null object
    borrower                    485 non-null object
    closingdate                 370 non-null object
    country_namecode            500 non-null object
    countrycode                 500 non-null object
    countryname                 500 non-null object
    countryshortname            500 non-null object
    docty                       446 non-null object
    envassesmentcategorycode    430 non-null object
    grantamt                    500 non-null int64
    ibrdcommamt                 500 non-null int64
    id                          500 non-null object
    idacommamt                  500 non-null int64
    impagency                   472 non-null object
    lendinginstr                495 non-null object
    lendinginstrtype            495 non-null object
    lendprojectcost             500 non-null int64
    majorsector_percent         500 non-null object
    mjsector_namecode           500 non-null object
    mjtheme                     491 non-null object
    mjtheme_namecode            500 non-null object
    mjthemecode                 500 non-null object
    prodline                    500 non-null object
    prodlinetext                500 non-null object
    productlinetype             500 non-null object
    project_abstract            362 non-null object
    project_name                500 non-null object
    projectdocs                 446 non-null object
    projectfinancialtype        500 non-null object
    projectstatusdisplay        500 non-null object
    regionname                  500 non-null object
    sector                      500 non-null object
    sector1                     500 non-null object
    sector2                     380 non-null object
    sector3                     265 non-null object
    sector4                     174 non-null object
    sector_namecode             500 non-null object
    sectorcode                  500 non-null object
    source                      500 non-null object
    status                      500 non-null object
    supplementprojectflg        498 non-null object
    theme1                      500 non-null object
    theme_namecode              491 non-null object
    themecode                   491 non-null object
    totalamt                    500 non-null int64
    totalcommamt                500 non-null int64
    url                         500 non-null object
    dtypes: int64(7), object(43)
    memory usage: 195.4+ KB
    None
    


```python

print(df.head())

```

                                        _id  approvalfy board_approval_month  \
    0  {'$oid': '52b213b38594d8a2be17c780'}        1999             November   
    1  {'$oid': '52b213b38594d8a2be17c781'}        2015             November   
    2  {'$oid': '52b213b38594d8a2be17c782'}        2014             November   
    3  {'$oid': '52b213b38594d8a2be17c783'}        2014              October   
    4  {'$oid': '52b213b38594d8a2be17c784'}        2014              October   
    
          boardapprovaldate                                 borrower  \
    0  2013-11-12T00:00:00Z  FEDERAL DEMOCRATIC REPUBLIC OF ETHIOPIA   
    1  2013-11-04T00:00:00Z                    GOVERNMENT OF TUNISIA   
    2  2013-11-01T00:00:00Z   MINISTRY OF FINANCE AND ECONOMIC DEVEL   
    3  2013-10-31T00:00:00Z   MIN. OF PLANNING AND INT'L COOPERATION   
    4  2013-10-31T00:00:00Z                      MINISTRY OF FINANCE   
    
                closingdate                              country_namecode  \
    0  2018-07-07T00:00:00Z  Federal Democratic Republic of Ethiopia!$!ET   
    1                   NaN                      Republic of Tunisia!$!TN   
    2                   NaN                                   Tuvalu!$!TV   
    3                   NaN                        Republic of Yemen!$!RY   
    4  2019-04-30T00:00:00Z                       Kingdom of Lesotho!$!LS   
    
      countrycode                              countryname    countryshortname  \
    0          ET  Federal Democratic Republic of Ethiopia            Ethiopia   
    1          TN                      Republic of Tunisia             Tunisia   
    2          TV                                   Tuvalu              Tuvalu   
    3          RY                        Republic of Yemen  Yemen, Republic of   
    4          LS                       Kingdom of Lesotho             Lesotho   
    
       ...   sectorcode source  status  supplementprojectflg  \
    0  ...  ET,BS,ES,EP   IBRD  Active                     N   
    1  ...        BZ,BS   IBRD  Active                     N   
    2  ...           TI   IBRD  Active                     Y   
    3  ...           JB   IBRD  Active                     N   
    4  ...     FH,YW,YZ   IBRD  Active                     N   
    
                                                  theme1  \
    0      {'Percent': 100, 'Name': 'Education for all'}   
    1  {'Percent': 30, 'Name': 'Other economic manage...   
    2    {'Percent': 46, 'Name': 'Regional integration'}   
    3  {'Percent': 50, 'Name': 'Participation and civ...   
    4  {'Percent': 30, 'Name': 'Export development an...   
    
                                          theme_namecode    themecode   totalamt  \
    0      [{'code': '65', 'name': 'Education for all'}]           65  130000000   
    1  [{'code': '24', 'name': 'Other economic manage...        54,24          0   
    2  [{'code': '47', 'name': 'Regional integration'...  52,81,25,47    6060000   
    3  [{'code': '57', 'name': 'Participation and civ...        59,57          0   
    4  [{'code': '45', 'name': 'Export development an...        41,45   13100000   
    
      totalcommamt                                                url  
    0    130000000  http://www.worldbank.org/projects/P129828/ethi...  
    1      4700000  http://www.worldbank.org/projects/P144674?lang=en  
    2      6060000  http://www.worldbank.org/projects/P145310?lang=en  
    3      1500000  http://www.worldbank.org/projects/P144665?lang=en  
    4     13100000  http://www.worldbank.org/projects/P144933/seco...  
    
    [5 rows x 50 columns]
    


```python
# Find the 10 countries with most projects
project_country = df['countryname'].value_counts().sort_values(ascending = False)
print(project_country[:10])
```

    Republic of Indonesia              19
    People's Republic of China         19
    Socialist Republic of Vietnam      17
    Republic of India                  16
    Republic of Yemen                  13
    Nepal                              12
    People's Republic of Bangladesh    12
    Kingdom of Morocco                 12
    Africa                             11
    Republic of Mozambique             11
    Name: countryname, dtype: int64
    


```python
#Find the top 10 major project themes (using column 'mjtheme_namecode')
print(df['mjtheme_namecode'])
```

    0      [{'code': '8', 'name': 'Human development'}, {...
    1      [{'code': '1', 'name': 'Economic management'},...
    2      [{'code': '5', 'name': 'Trade and integration'...
    3      [{'code': '7', 'name': 'Social dev/gender/incl...
    4      [{'code': '5', 'name': 'Trade and integration'...
    5      [{'code': '6', 'name': 'Social protection and ...
    6      [{'code': '2', 'name': 'Public sector governan...
    7      [{'code': '11', 'name': 'Environment and natur...
    8      [{'code': '10', 'name': 'Rural development'}, ...
    9      [{'code': '2', 'name': 'Public sector governan...
    10     [{'code': '10', 'name': 'Rural development'}, ...
    11     [{'code': '10', 'name': 'Rural development'}, ...
    12                           [{'code': '4', 'name': ''}]
    13     [{'code': '5', 'name': 'Trade and integration'...
    14     [{'code': '6', 'name': 'Social protection and ...
    15     [{'code': '10', 'name': 'Rural development'}, ...
    16     [{'code': '10', 'name': 'Rural development'}, ...
    17     [{'code': '8', 'name': 'Human development'}, {...
    18     [{'code': '8', 'name': 'Human development'}, {...
    19     [{'code': '2', 'name': 'Public sector governan...
    20     [{'code': '7', 'name': 'Social dev/gender/incl...
    21     [{'code': '9', 'name': 'Urban development'}, {...
    22     [{'code': '7', 'name': 'Social dev/gender/incl...
    23     [{'code': '8', 'name': 'Human development'}, {...
    24     [{'code': '10', 'name': 'Rural development'}, ...
    25     [{'code': '11', 'name': 'Environment and natur...
    26     [{'code': '4', 'name': 'Financial and private ...
    27     [{'code': '11', 'name': 'Environment and natur...
    28     [{'code': '10', 'name': 'Rural development'}, ...
    29     [{'code': '7', 'name': 'Social dev/gender/incl...
                                 ...                        
    470    [{'code': '5', 'name': 'Trade and integration'...
    471    [{'code': '10', 'name': 'Rural development'}, ...
    472    [{'code': '11', 'name': 'Environment and natur...
    473    [{'code': '11', 'name': 'Environment and natur...
    474    [{'code': '9', 'name': 'Urban development'}, {...
    475    [{'code': '4', 'name': 'Financial and private ...
    476    [{'code': '10', 'name': 'Rural development'}, ...
    477    [{'code': '4', 'name': 'Financial and private ...
    478    [{'code': '2', 'name': 'Public sector governan...
    479    [{'code': '7', 'name': 'Social dev/gender/incl...
    480    [{'code': '2', 'name': 'Public sector governan...
    481    [{'code': '8', 'name': 'Human development'}, {...
    482    [{'code': '10', 'name': 'Rural development'}, ...
    483    [{'code': '11', 'name': 'Environment and natur...
    484    [{'code': '10', 'name': 'Rural development'}, ...
    485    [{'code': '8', 'name': 'Human development'}, {...
    486    [{'code': '2', 'name': 'Public sector governan...
    487    [{'code': '11', 'name': 'Environment and natur...
    488    [{'code': '8', 'name': 'Human development'}, {...
    489    [{'code': '9', 'name': 'Urban development'}, {...
    490    [{'code': '2', 'name': 'Public sector governan...
    491    [{'code': '10', 'name': 'Rural development'}, ...
    492    [{'code': '8', 'name': 'Human development'}, {...
    493    [{'code': '11', 'name': 'Environment and natur...
    494    [{'code': '6', 'name': 'Social protection and ...
    495    [{'code': '4', 'name': 'Financial and private ...
    496    [{'code': '8', 'name': 'Human development'}, {...
    497    [{'code': '10', 'name': 'Rural development'}, ...
    498    [{'code': '10', 'name': 'Rural development'}, ...
    499    [{'code': '9', 'name': 'Urban development'}, {...
    Name: mjtheme_namecode, Length: 500, dtype: object
    


```python
#Extract 'mjtheme_namecode' into multiple columns using json_normalization
df_list = json.load(open('world_bank_projects.json'))

mjtheme_namecode = json_normalize(df_list, 'mjtheme_namecode')

#Print head to make sure data is in the proper format
print(mjtheme_namecode.head())
```

      code                                   name
    0    8                      Human development
    1   11                                       
    2    1                    Economic management
    3    6  Social protection and risk management
    4    5                  Trade and integration
    


```python
#Find the top 10 themes
theme_names = mjtheme_namecode['name'].value_counts().sort_values(ascending = False)
print(theme_names[:10])
```

    Environment and natural resources management    223
    Rural development                               202
    Human development                               197
    Public sector governance                        184
    Social protection and risk management           158
    Financial and private sector development        130
                                                    122
    Social dev/gender/inclusion                     119
    Trade and integration                            72
    Urban development                                47
    Name: name, dtype: int64
    


```python
#3) Create a dataframe with the missing names filled in.
#Check the data type of each column
print(mjtheme_namecode.info())
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1499 entries, 0 to 1498
    Data columns (total 2 columns):
    code    1499 non-null object
    name    1499 non-null object
    dtypes: object(2)
    memory usage: 23.5+ KB
    None
    


```python
#The code column is object instead of integer
mjtheme_namecode['code'] = pd.to_numeric(mjtheme_namecode['code'])
#Check to see if the data type has changed
print(mjtheme_namecode.info())
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1499 entries, 0 to 1498
    Data columns (total 2 columns):
    code    1499 non-null int64
    name    1499 non-null object
    dtypes: int64(1), object(1)
    memory usage: 23.5+ KB
    None
    


```python
#Now the data is ready to manipulate
#First replace blank entries with NaN
mjtheme_namecode_NaN = mjtheme_namecode.replace('', np.nan)

#Sort based on code. First sort by code then on name
mjtheme_namecode_NaN = mjtheme_namecode_NaN.sort_values(['code', 'name'])
print(mjtheme_namecode_NaN[:50])
```

          code                      name
    2        1       Economic management
    88       1       Economic management
    175      1       Economic management
    204      1       Economic management
    205      1       Economic management
    220      1       Economic management
    222      1       Economic management
    223      1       Economic management
    249      1       Economic management
    357      1       Economic management
    453      1       Economic management
    454      1       Economic management
    458      1       Economic management
    497      1       Economic management
    647      1       Economic management
    648      1       Economic management
    784      1       Economic management
    803      1       Economic management
    841      1       Economic management
    900      1       Economic management
    1010     1       Economic management
    1045     1       Economic management
    1056     1       Economic management
    1057     1       Economic management
    1078     1       Economic management
    1206     1       Economic management
    1212     1       Economic management
    1218     1       Economic management
    1229     1       Economic management
    1230     1       Economic management
    1235     1       Economic management
    1257     1       Economic management
    1260     1       Economic management
    212      1                       NaN
    363      1                       NaN
    1024     1                       NaN
    1114     1                       NaN
    1437     1                       NaN
    5        2  Public sector governance
    14       2  Public sector governance
    20       2  Public sector governance
    21       2  Public sector governance
    22       2  Public sector governance
    45       2  Public sector governance
    48       2  Public sector governance
    49       2  Public sector governance
    50       2  Public sector governance
    68       2  Public sector governance
    71       2  Public sector governance
    90       2  Public sector governance
    


```python
#We see that that the NaN entries occur at the end of the of the entries with code = 1
#Using ffill will insert the last valid value to the NaN entries
mjtheme_namecode_full = mjtheme_namecode_NaN.fillna(method='ffill')

print(mjtheme_namecode_full.head(50))
```

          code                      name
    2        1       Economic management
    88       1       Economic management
    175      1       Economic management
    204      1       Economic management
    205      1       Economic management
    220      1       Economic management
    222      1       Economic management
    223      1       Economic management
    249      1       Economic management
    357      1       Economic management
    453      1       Economic management
    454      1       Economic management
    458      1       Economic management
    497      1       Economic management
    647      1       Economic management
    648      1       Economic management
    784      1       Economic management
    803      1       Economic management
    841      1       Economic management
    900      1       Economic management
    1010     1       Economic management
    1045     1       Economic management
    1056     1       Economic management
    1057     1       Economic management
    1078     1       Economic management
    1206     1       Economic management
    1212     1       Economic management
    1218     1       Economic management
    1229     1       Economic management
    1230     1       Economic management
    1235     1       Economic management
    1257     1       Economic management
    1260     1       Economic management
    212      1       Economic management
    363      1       Economic management
    1024     1       Economic management
    1114     1       Economic management
    1437     1       Economic management
    5        2  Public sector governance
    14       2  Public sector governance
    20       2  Public sector governance
    21       2  Public sector governance
    22       2  Public sector governance
    45       2  Public sector governance
    48       2  Public sector governance
    49       2  Public sector governance
    50       2  Public sector governance
    68       2  Public sector governance
    71       2  Public sector governance
    90       2  Public sector governance
    


```python
print(mjtheme_namecode_full.info())
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 1499 entries, 2 to 1477
    Data columns (total 2 columns):
    code    1499 non-null int64
    name    1499 non-null object
    dtypes: int64(1), object(1)
    memory usage: 35.1+ KB
    None
    


```python
theme_names_full =mjtheme_namecode_full['name'].value_counts().sort_values(ascending = False)
print(theme_names_full[:10])
```

    Environment and natural resources management    250
    Rural development                               216
    Human development                               210
    Public sector governance                        199
    Social protection and risk management           168
    Financial and private sector development        146
    Social dev/gender/inclusion                     130
    Trade and integration                            77
    Urban development                                50
    Economic management                              38
    Name: name, dtype: int64
    


```python

```


```python

```
