[View in Mermaid Live Editor (features pan and zoom)](https://mermaid.live/edit#pako:eNrNWFtv2zYU_isEgQIt4BhOHNeOX4oBQV-KocPap0GAQEtHMTeJVEkqqxb7v--QkhxRF1tJ9jA_2DB5vo_nziM90UjGQLcU1D1nD4plgQjEu3fkvhQs4xGROShmuBQsJTEzbBuIQoMiT4Eg-NFGcfFAeEx--0IC6rZ4DMLwhIMKqCelZArk8xdvTaoIwQEVRZqyXQodyI5LVCrfl94qSxKecqcWQj9ZzNHqrUDnUmhotCsK5Ha61XD4QR5BaYuzax4p_ERTTWhNCBHT0ZPlecojd2Qod39CZBqhSowpxUpi2IPu0EYKmIE43JUnSvQjGJ5Bs9dZLfK4WnU2PVuF56Juj0ga6lIbyBozuTDkJNQ2txUc3-kDBoAoMmLKHDzJQqW-GwqzlyrE3IChdcgY9wFJIWKrcSQLYVQ5uMceQET-loIEFK6CDiNunNu1JyCkAd3Jm2Odu9_3XBOrIsHfSIqk0AiZkV1hEFF5sc7pgJKQ65AwZzqRCTk5mVROPuP_0KOaGI0eSS3iCeUpM4lUmbeoQWipOqneVwp3gKlo_2Z9_CQSBlQGMVYdhLmScRGZi6rYhtEIv1Gdlkib1fee5e4RYAIgDmNvS9dIT6nQ9jakDOji6nqxaJqP5dG4oxMWOdiwWJOrdQLAeBsTADH2AJ7huY-QYX8czN2TX17huMtVPtm2cV3CVhucqNdQtEb6ai-WHrYbxzbyfxrGAW_50Rr24OdzcRw9IdQy4mBYGu5AQMIxWHi9TIzSILYfkPZx3XhYCmwOXY6R9PLahrVvZKJwN40fBdepGx99_3r_tfoKaCYVEJw70lh_ah3EMKilxqtg8gkVYnQWiEFHiufWcHdIc0DYnT88Otzv-70bklplvMS-2Vsver4Im-mr47bQeeO8ZUh6NjdeANPFbgJySmLVudzb_wvK2jT-CG84p9a0dZQbPy-afArA75BWc8ee57qeeo-Hq6vDwQ2yW4RZSGvqPEq3ayWb3e5eJ3oDJAc8Qj6R0Uu1x9wFtJvmReFWQb9EdrjX9K3pj6yNB4f9MI5zyhzIxFnsP-BrxqgBo7zb-bxBI5fBJdBYwVqtD0-jyd4QjJbtGN4ruvO6h2c0O5DpeeF6_rAfXE97Bp36dy3dri9Xqb_o6u6xDUO1q5a853OYd9b-5mbvmumHS_lxOFOGZ8vMz5BXUU0lG5vOeiq10--lJBNpXtEgXEyxyfSu0EbUC_64IJ3RDJ9PGI_plroeH1CzB9vVrUAMCStS41o8iuLTqvxWiohuE5ZqmNHqkbt-A3JazZn4Q0r8b1RR_aXbJ_qTbq-uV8v5x9ub25vVarm-XtwtNzNa0u16Pd98XN0slpvV-vbmerM5zug_juF6vrjd3K6Xd4vl3erubr1czSg-TBmpfq3ev7jXMMd_AXhuXOo)


```mermaid
erDiagram

%% Dynamic operational data:
user {
    string id PK "user identifier"
    string role FK
    string orcid "nullable"
    string biography
    string affiliation "?"
}

response {
    uuid id PK
    seq version PK

    string expert_user_id FK
    string application_object_id FK

    array tags

    string created_by FK
    datetime created
    datetime updated
}


response_observing_system {
    int response_id PK
    string id PK
    string object_id FK

    enum type
    string url
    string author_name
    string author_email
    string funding_country
    string funding_agency
    string references_citations
    string notes "nullable"
}

%% This name is confusing, but "observational" _is_ a type of observing system
response_observing_system_observational {
    int response_id PK
    string observing_system_id PK

    string platform
    string sensor
}

response_observing_system_research {
    int response_id PK
    string observing_system_id PK


    string intermediate_product
}

response_observing_system_data_product {
    int response_id PK
    string observing_system_id PK
    string data_product_id PK

    int observing_system_contribution_to_data_product_rating "0-100"
    int satisfaction_rating "0-100"
    string rationale "nullable"
    string needed_improvements "nullable"
}

response_data_product {
    int response_id PK
    string id PK
    string object_id FK


    int satisfaction_rating "0-100"
}

response_data_product_application {
    int response_id PK
    string data_product_id PK
    string application_id PK

    int data_product_contribution_to_application_rating "0-100"
    int satisfaction_rating "0-100"
    string rationale "nullable"
    string needed_improvements "nullable"
}

response_application {
    string id PK

    int response_id FK
    string object_id FK
}

response_application_societal_benefit_area {
    int response_id PK
    string societal_benefit_area_id PK

    int application_contribution_to_sociateal_benefit_area_rating "0-100"
}


response_object {
    string id PK "name"
    string type FK
    TODO TODO "more fields?"
}


analysis {
    string id PK "name"
    string analyst_user_id FK
    string description
}
analysis_response {
    string analysis_id PK
    string response_id PK
}


%% Static reference data:
response_object_type {
    string id PK "name"
}
societal_benefit_area {
    string id PK "name"
}
societal_benefit_subarea {
    string id PK "name"
    string societal_benefit_area_id FK
}
societal_benefit_key_objective {
    string id PK "name"
    string societal_benefit_subarea_id FK
}
role {
    string id PK "name"
}



%% Relationships
user }|--|| role: ""

response }o--|| user: ""
response }o--|| response_object: ""

response ||--o{ response_observing_system: ""
response ||--o{ response_data_product: ""
response ||--o{ response_application: ""
response ||--o{ response_application_societal_benefit_area: ""

response_observing_system }|--|| response_object: ""
response_observing_system ||--o| response_observing_system_observational: ""
response_observing_system ||--o| response_observing_system_research: ""

response_data_product }|--|| response_object: ""

response_application }|--|| response_object: ""


societal_benefit_area ||--|{ societal_benefit_subarea: ""
societal_benefit_subarea ||--|{ societal_benefit_key_objective: ""

response_application_societal_benefit_area ||--|| societal_benefit_area: ""

response_object }|--|| response_object_type: ""

analysis }|--|| user: ""

%% Associative relationships (i.e. relationships with data)
response_observing_system ||--|{ response_observing_system_data_product: ""
response_data_product ||--|{ response_observing_system_data_product: ""

response_data_product ||--|{ response_data_product_application: ""
response_application ||--|{ response_data_product_application: ""

response_application ||--|{ response_application_societal_benefit_area: ""

response }|--o{ analysis_response: ""
analysis }|--o{ analysis_response: ""
```
