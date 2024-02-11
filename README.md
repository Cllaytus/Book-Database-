import pandas as pd

import numpy as np

book={
        'BookId':['BO1','B24','B861','B233','B315','B207','B074','B450','B965'],
        'Title':['Painted House','Abduction','Airport','Invasion','Prizes','Icon','The Simple Truth','The Class','Doomsday Conspiracy'],
        'AuthorId':['A21','AD1','A27','AD1','A301','A21','A301','A21','A33'],
        'PubId':['P22','P078','P279','P078','P279','P610','P22','P12','P22'],
        'Year':[2001,2000,1968,1997,1995,1996,1997,1985,1978],
        'Price':[195.55,360,175.45,177.9,256.1,182.35,211.0,145.8,225.50]}

Table1=pd.DataFrame(book)
Table1.head(10)

author={'Id':['A21','A01','A27','A301','A478'],
        'Name':['Grisham','Cook','Hally','Segal','Forsyth'],
        'City':['New York','London','Manchester','Houston','New York'],
        'Country':['United States','United Kingdom','United Kingdom','United States','United States']}

Table2=pd.DataFrame(author)
Table2.head()

publisher={'Id':['P22','P610','P078','P279','P12','P29'],
           'Name':['Random House','Dell Books','Pan Books','Signet Books','Macmillan','Madhavan'],
           'City':['Las Vegas','Colorado','London','Aberdeen','London','Aberdeen'],
           'Country':['Unites States','United States','United Kingdom','United Kingdom','United Kingdom','United Kingdom']}


Table3=pd.DataFrame(publisher)
Table3.head(10)

# 1. DISPLAY THE BOOKS WRITTEN BY SEGAL OR GRISHAM

a1=pd.merge(Table1, Table2, left_on= "AuthorId", right_on= "Id", how= "inner")
aa1=a1[(a1["Name"] =="Segal") |(a1["Name"]=="Grisham")]
aa1[["Title","Name"]]
b1=pd.merge(Table1, Table2, left_on= "AuthorId", right_on= "Id")
bb1=a1[a1["Name"].isin(["Segal","Grisham"])]
bb1[["Title","Name"]]

# 2. DISPLAY THE BOOKS WRITTEN BY SIGNET BOOKS

a2=pd.merge(Table1, Table3, left_on= "PubId", right_on= "Id", how= "inner")
aa2=a2[(a2["Name"] =="Signet Books")]
aa2[["Title","Name"]]


# 3.  DISPLAY THE BOOKS WRITTEN BY GRISHAM AND PUBLISHED BY MACMILLAN


a3 = pd.merge(Table1, Table2, left_on= "AuthorId", right_on= "Id",how="inner")
b3=pd.merge(a3,Table3,left_on="PubId",right_on="Id",how="outer")
c3=b3[(b3["Name_x"] =="Grisham") & (b3["Name_y"]=="Macmillan")]
c3  

# 4. DISPLAY THE BOOK DETAILS AND PUBLISHER DETAILS WHO PUBLISHED BOOKS FROM 2000S

a4=pd.merge(Table1, Table3, left_on= "PubId", right_on= "Id", how= "inner")
b4=a4[a4["Year"]>=2000]
b4

# 5. DISPLAY THE AUTHOR DETAILS AND NUMBER OF BOOKS WRITTEN

a5=pd.merge(Table1, Table2, left_on= "AuthorId", right_on= "Id", how= "inner")
b5=a5["Name"].value_counts().reset_index(name="BookId")
c5=b5.rename(columns={"Name":"Author","BookId":"Number_Of_Books"})
c5

# 6. DISPLAY THE AUTHOR AND PUBLISHER WITH THE HIGHEST PRICE OF BOOKS

a6 = pd.merge(Table1, Table2, left_on= "AuthorId", right_on= "Id",how="inner")
a6
b6=a6.groupby(['Id','Name']).agg({'Price':'max'}).reset_index()
b6

#  7. DISPLAY THE DETAILS OF THE AUTHORS AND THE PUBLISHERS 

a7 = pd.merge(Table1, Table2, left_on= "AuthorId", right_on= "Id",how="inner")
b7=pd.merge(a7,Table3,left_on="PubId",right_on="Id",how="outer")
c7=b7.rename(columns={"Name_x":"Author_Name","City_x":"Authors_City","Idy_x":"AuthorId","Country_x":"Author_Country","Name_y":"Publisher_Name","City_y":"Publisher_City","Idy_y":"PublisherId","Country_y":"Publisher_Country"})
c7


#  8. LIST THE DETAILS OF THE AUTHOR AND PUBLISHER WHO RESIDES IN LONDON AND COLORADO RESPECTIVELY

a8 = pd.merge(Table1, Table2, left_on= "AuthorId", right_on= "Id")
b8=pd.merge(a8,Table3,left_on="PubId",right_on="Id")
c8=b8[b8['City_y']=='Colorado'][['Name_y','City_y','Country_y']]
d8=b8[b8['City_y']=='London'][['Name_y','City_y','Country_y']]
e8=pd.concat([c8,d8],ignore_index=True)
e8

# 9. LIST THE DISTINCT CITIES FROM AUTHORS TABLE AND PUBLISHERS TABLE

a9=Table2['City'].unique()
b9=Table3['City'].unique()
c9=[a9,b9]
c9

#  10. MERGE THE RECORDS IN AUTHORS TABLE WITH PUBLISHERS TABLE

a10 = pd.concat([Table2,Table3],ignore_index=True)
a10


