```mermaid
erDiagram

%% Dynamic operational data:
user {
    string id PK "user identifier"
    string role FK
}

response {
    uuid id FK "unique"
    string user_id FK
    datetime updated
}

response_object {
    string id PK "name"
    string type FK
    TODO TODO "more fields?"
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
    int response_id PK
    string id PK
    string object_id FK
}

response_application_societal_benefit_area {
    int response_id PK
    string societal_benefit_area_id PK

    int application_contribution_to_sociateal_benefit_area_rating "0-100"
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

%% Associative relationships (i.e. relationships with data)
response_observing_system ||--|{ response_observing_system_data_product: ""
response_data_product ||--|{ response_observing_system_data_product: ""

response_data_product ||--|{ response_data_product_application: ""
response_application ||--|{ response_data_product_application: ""

response_application ||--|{ response_application_societal_benefit_area: ""
```

[View in Mermaid Live Editor](https://mermaid.ink/img/pako:eNrNWEtv4zYQ_isEgQVawDH8iJ2sL0WBYC-LYovungoBAi2NYrYSqZJUumrs_94hJTmiHraS9NAcHIgz83HeM9IzjWQMdEdBPXD2qFgWiEB8-EAeSsEyHhGZg2KGS8FSEjPDdoEoNCjyHAiCf9ooLh4Jj8mvn0lAHYnHIAxPOKiAelxKpkA-ffbOpIpQOKCiSFO2T6EjsucSlcoPpXfKkoSn3KmFoj9ZmZPVW4HOpdAQyv0fEJkRJdGw7jWmzF80-_bl4Uv1E9BMKiBoShrr_jUNflEgtEOvQeEv8gRKW_XsmXcVfEePmtB6KkSZjjtYnqc8cpbVRjRMFRtTipXEsEfdgY0UMANxuC_PkBguMDyDhtY5LfK4OnU2ec5D3Z4QNNSlNpA1ZnJhyJmpbW7LvX5sBwwAUWTO3R5noVLfDYU5SBW6SA2cQ8a4L5AUIrYaR7IQRpWDNPYIIvJJChJQeAo6jLhxbtceg5AGdCc9T3WJfDtwTayKBP9HUiSFRpEZ2RcGJSov1qUTUBJyHRJWZZpMyNnJpHLyBf-HHtTEaPRAahaPKU-ZSaTKvEMNQkvVr6gOHlKAqejwbn38JBIGVAYxFjeEuZJxEZmrqti-1DC_U50WSxvV957F7gFgAqAcxt6WrpGeUqFtoQgZ0MXNcrFomo_F0UjRCYuc2DBbk6t1AsB4txQAMfYAnuG9T5BhGx7M3bNf3uC461U-2bZxXcJWG5yo11C0RvpqL5aebDeObcn_aRgHvOVHa9iDny7FcfSGUMuIg2FpuAcBCcdg4XiZGKVB2X5A2td142EhsDl0MUbSi6GnS439efIqUEmMDugYdKR4brVxVzQXhN2lwINDet8ZXT_Vcxgny1c7iqKX6dRsXp39JnTD5LJlCHoxYK8Q08V-guSUaNcJ1qP_CWVtGn-Cd9xTa9q6yq2eV00-B-A3SKtl4MBzXW-8p-PNzfHoltgdilmR1ip4ko5qORtql9aJ3gDIEa-Qz2R00vWQuwLtTnaVuVVlr-EdbgB9a_p7ZOPBYT-MyzlljmTigvQf4DW7zYBR3si8bNBIh74mNFawVuvj82iyNwCjZTsm7xXdZd3DC5odyfS8cC9nw35wPe1F6Ny_a-52fblK_VlXA8E2DNWuWvIDn8O8c_Y3NwfXTH-8lh_HC2V4scz8DHkT1FSwsZWpp1I7_V4LMhHmDQ3CxRSbTG-ENqxe8McZ6Yxm-NLAeEx31PX4gJoD2K5uGWJIWJEa1-KRFV8h5ddSRHSXsFTDjFbvwfXXj_NpzsTvUuKzUUX1SHfP9Dvd3Wy2q_n69n613W4XS3zYzGhJd9vlfLFd3y9Xq83mfvNxfbc5zeg_DmE136zvtve3d7e3q-UaKbczim84Rqpfqm8v7hPM6V_eI1tF)
