# AreaX-Blood-Bank

Joanna Getek  

Brenda Huppenthal  

CS340 - Oregon State University

## Project Outline ##
Fake Medical Center (FMC), an 800 bed level I trauma hospital, provides over 50,000 units of
blood products to patients in the hospital each year and employs approximately 5,000 staff
members. Depending on the patient’s medical condition they can potentially receive over a
dozen blood products during an inpatient stay. Currently, the hospital’s blood bank uses
outdated paper based records to store blood product information and to chart the dispensing of
blood products for administration to inpatients. The process is time consuming for medical lab
technicians, physicians, and nurses. Additionally, paper charting and information storage
creates more room for medical errors due to inconsistency, illegible writing, limited access and
disorganization of medical records.
Our database driven front end will allow an easier, quicker, and safer method of recording
life-saving blood transfusions to patients. The application will adhere to the highest quality and
safety standards.
The database will contain information about the blood product stored in the hospital’s blood
bank to be dispensed. The patient that will be receiving the blood transfusion as well as the
nurse that will be administering the blood product will also be entities in the database. The
transfusion order entity will outline the details of the blood product administration. Lastly, the
type of blood product and blood type will be entities in the database to provide clear descriptions
to the users. Please note that these are highly idealized entities.

## Database Outline ## 
### Object Tables:  

**BloodProducts**: records the details of the blood products to be dispensed  
- BloodProductID: int, auto_increment, unique, not null, primary key  
- ProductTypeID: varchar, not null, foreign key  
- BloodTypeID: varchar, not null, foreign key  
- DrawnDate: datetime  
- ExpirationDate: datetime, not null  
- DonorID: int, not null  
- Volume: int, in mL
  
  **Relationships**:  
  - **TransfusionOrders**: M to M, as a single transfusion order may list several blood
  products, and blood products may be split between transfusion orders
  - **ProductTypes**: M to 1, as many blood products will be of the same type (i.e. there
  will be many bags of red blood cells)
  - **BloodTypes**: M to 1, as a single blood product can only have one blood type but a
  single blood type can apply to many different blood products



**Patients**: records the details of the patients in the hospital  
- PatientID: int, auto_increment, unique, not null, primary key
- Name: varchar, unique, not null
- BirthDate: date, not null
- MedicalRecordNumber: int, unique, not null
- BloodTypeID: varchar, foreign key


  **Relationships**:
  - **TransfusionOrders**: 1 to M, as one patient can have many transfusions
  - **BloodTypes**: M to 1, as many patients can have the same blood type, but each
  patient can only have one blood type


**Nurses**: records the details of the nurses who work in the hospital  
- NurseID: int, auto_increment, unique, not null, primary key
- Name: varchar, unique
- Extension: int, unique  

  **Relationships**:
  - **TransfusionOrders**: 1 to M with transfusion orders, as the nurse may perform 0 or
  more transfusions


### Transaction Table:  
**TransfusionOrders**: records the details of a transfusion given to a patient  
- TransfusionID: int, auto_increment, unique, not null, primary key
- PatientID: int, not null, foreign key
- NurseID: int, not null, foreign key
- Date: datetime, not null
- Description: varchar
- InfusionRate: decimal, not null

  **Relationships**:
  - **Nurses**: M to 1 with nurse, as each transfusion order can only have one nurse’s
  name attached to it
  - **Patients**: M to 1 with patient, as each transfusion order can only list one patient to
  receive the transfusion
  - **BloodProducts**: M to M with blood product, as a single transfusion order may list
  several blood products, and blood products may be split between transfusion
  orders  

### Category Tables:
**ProductTypes**: product given to patients such as red blood cells, cryo, plasma  
- ProductTypeID: varchar, unique, not null, primary key
  - Type of the blood product: red blood cells, plasma, cryo, platelets
    
  **Relationships**:
  ● **BloodProducts**: 1 to M with as a single ProductType can be associated with many
  different blood products, but a single blood product can have only one product
  type
  

**BloodTypes**: blood type of patients/products, based on A/B antigens and Rh factor
- BloodTypeID: varchar, unique, not null, primary key
  - (ABO & Rh): A/B/AB/O and +/-
 
  **Relationships**:
  - **BloodProducts**: 1 to M as a BloodType can be associated with many
  different blood products, but a single blood product can only have one blood type
  - **Patients**: 1 to M as a BloodType can be associated with many patients, but a
  patient can only have one blood type

### Intersection Table:  
**TransfusionDetails**: intersection table for the M:M relationship between the
TransfusionOrders and the BloodProducts  

- TransfusionDetailID: int, auto_increment, unique, not null, primary key
- TransfusionID: int, not null, foreign key
- BloodProductID: int, not null, foreign key
- Volume: decimal, not null

  **Relationships**:
  - **TransfusionOrders**: M:1 as each transfusion order may be associated with
  multiple transfusion details
  - **BloodProducts**:  M:1 as each blood product may be associated with multiple
  transfusion details

<img width="459" alt="image" src="https://github.com/getekj/AreaX-Blood-Bank/assets/97110548/f4ba76e1-839a-4768-a79c-a344c6f28ac0">

<img width="474" alt="image" src="https://github.com/getekj/AreaX-Blood-Bank/assets/97110548/b7531da8-4829-465b-bedb-b9dded205123">

<img width="483" alt="image" src="https://github.com/getekj/AreaX-Blood-Bank/assets/97110548/e85d5deb-9e15-4cc8-9b17-b3a93d1d1b76">

<img width="479" alt="image" src="https://github.com/getekj/AreaX-Blood-Bank/assets/97110548/3eb21ec5-05fa-4349-8097-271ac9bd1c0a">

<img width="483" alt="image" src="https://github.com/getekj/AreaX-Blood-Bank/assets/97110548/44088469-3073-490a-917d-eb739fe145dd">

<img width="476" alt="image" src="https://github.com/getekj/AreaX-Blood-Bank/assets/97110548/ce429d99-df0f-417a-b3f7-974fa2ddd7d2">

<img width="489" alt="image" src="https://github.com/getekj/AreaX-Blood-Bank/assets/97110548/3bf8f498-e027-422c-beb7-9e52781332ae">

<img width="574" alt="image" src="https://github.com/getekj/AreaX-Blood-Bank/assets/97110548/b34a29f2-ddf4-4272-90f9-7de97f1421ed">

<img width="574" alt="image" src="https://github.com/getekj/AreaX-Blood-Bank/assets/97110548/2dcff007-cc6e-4471-959f-d7baff3b540d">
