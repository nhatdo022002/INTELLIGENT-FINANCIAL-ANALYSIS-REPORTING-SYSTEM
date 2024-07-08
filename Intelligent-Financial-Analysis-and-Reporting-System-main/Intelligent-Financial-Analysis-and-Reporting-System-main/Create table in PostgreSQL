-- Kiểm tra xem bảng DIM_COMPANY đã tồn tại hay chưa
SELECT 1
FROM pg_catalog.pg_tables
WHERE tablename = 'DIM_COMPANY'
AND schemaname = 'public';

-- Tạo bảng DIM_COMPANY nếu nó không tồn tại
CREATE TABLE IF NOT EXISTS public.DIM_COMPANY (
  COMPANY_ID VARCHAR(4) PRIMARY KEY,
  COMPANY_NAME VARCHAR(256),
  ADDRESS VARCHAR(256),
  DISTRICT varchar (30),
  PROVINCE Varchar(30)
);

--Tạo bảng DIM_DATE
DO $$
BEGIN
    -- Kiểm tra xem bảng DIM_DATE đã tồn tại hay chưa
    IF NOT EXISTS (
        SELECT 1
        FROM pg_catalog.pg_tables
        WHERE tablename = 'DIM_DATE'
        AND schemaname = 'public'
    ) THEN
        -- Tạo bảng DIM_DATE nếu nó không tồn tại
        CREATE TABLE dim_date (
            DATE_ID VARCHAR(10) PRIMARY KEY,
            DATE DATE NOT NULL,
            MONTH INT NOT NULL,
            MONTH_NAME VARCHAR(3) NOT NULL,
            QUARTER INT NOT NULL,
            QUARTER_NAME VARCHAR(2) NOT NULL,
            YEAR INT NOT NULL
        );
    END IF;
END $$;


-- Tạo bảng DIM_KQHDKD
DO $$
BEGIN
    -- Kiểm tra xem bảng DIM_KQHDKD đã tồn tại hay chưa
    IF NOT EXISTS (
        SELECT 1
        FROM pg_catalog.pg_tables
        WHERE tablename = 'DIM_KQHDKD'
        AND schemaname = 'public'
    ) THEN
        -- Tạo bảng DIM_KQHDKD nếu nó không tồn tại
        CREATE TABLE dim_kqhdkd (
            LEVEL1_NAME VARCHAR(256),
            LEVEL1_ID VARCHAR(4),
            LEVEL2_NAME VARCHAR(256) NOT NULL,
            LEVEL2_ID VARCHAR(4) PRIMARY KEY
        );
    END IF;
END $$;

--tạo bảng fact_KQHDKD
DO $$
BEGIN
    -- Kiểm tra xem bảng FACT_KQHDKD đã tồn tại hay chưa
    IF NOT EXISTS (
        SELECT 1
        FROM pg_catalog.pg_tables
        WHERE tablename = 'FACT_KQHDKD'
        AND schemaname = 'public'
    ) THEN
        -- Tạo bảng FACT_KQHDKD nếu nó không tồn tại
        CREATE TABLE FACT_KQHDKD (
            COMPANY_ID VARCHAR(4) NOT NULL REFERENCES DIM_COMPANY(COMPANY_ID),
            ID VARCHAR(4) NOT NULL REFERENCES DIM_KQHDKD(LEVEL2_ID),
            VALUE DECIMAL NOT NULL,
            DATE_ID VARCHAR(10) NOT NULL REFERENCES DIM_DATE(DATE_ID),
            CONSTRAINT FACT_KQHDKD_PK PRIMARY KEY (COMPANY_ID, ID, DATE_ID)
        );
    END IF;
END $$;

--Tạo bảng DIM_CDKT
DO $$
BEGIN
    -- Kiểm tra xem bảng DIM_KQHDKD đã tồn tại hay chưa
    IF NOT EXISTS (
        SELECT 1
        FROM pg_catalog.pg_tables
        WHERE tablename = 'DIM_CDKT'
        AND schemaname = 'public'
    ) THEN
        -- Tạo bảng DIM_CDKT nếu nó không tồn tại
        CREATE TABLE DIM_CDKT (
            LEVEL1_NAME VARCHAR(256),
            LEVEL1_ID VARCHAR(4),
			LEVEL2_NAME VARCHAR(256),
            LEVEL2_ID VARCHAR(4),
			LEVEL3_NAME VARCHAR(256),
            LEVEL3_ID VARCHAR(4),
			LEVEL4_NAME VARCHAR(256),
            LEVEL4_ID VARCHAR(4),
            LEVEL5_NAME VARCHAR(256) NOT NULL,
            LEVEL5_ID VARCHAR(4) PRIMARY KEY
        );
    END IF;
END $$;

--Tạo bảng FACT_CDKT

DO $$
BEGIN
    -- Kiểm tra xem bảng FACT_CDKT đã tồn tại hay chưa
    IF NOT EXISTS (
        SELECT 1
        FROM pg_catalog.pg_tables
        WHERE tablename = 'FACT_CDKT'
        AND schemaname = 'public'
    ) THEN
        -- Tạo bảng FACT_CDKT nếu nó không tồn tại
        CREATE TABLE FACT_CDKT (
            COMPANY_ID VARCHAR(4) NOT NULL REFERENCES DIM_COMPANY(COMPANY_ID),
            ID VARCHAR(4) NOT NULL REFERENCES DIM_CDKT(LEVEL5_ID),
            VALUE DECIMAL NOT NULL,
            DATE_ID VARCHAR(10) NOT NULL REFERENCES DIM_DATE(DATE_ID),
            CONSTRAINT FACT_CDKT_PK PRIMARY KEY (COMPANY_ID, ID, DATE_ID)
        );
    END IF;
END $$;


--Tạo bảg DIM_LCTT_GT
DO $$
BEGIN
    -- Kiểm tra xem bảng DIM_LCTT_GT đã tồn tại hay chưa
    IF NOT EXISTS (
        SELECT 1
        FROM pg_catalog.pg_tables
        WHERE tablename = 'DIM_LCTT_GT'
        AND schemaname = 'public'
    ) THEN
        -- Tạo bảng DIM_LCTT_GT nếu nó không tồn tại
        CREATE TABLE DIM_LCTT_GT (
            LEVEL1_NAME VARCHAR(256),
            LEVEL1_ID VARCHAR(4),
			LEVEL2_NAME VARCHAR(256),
            LEVEL2_ID VARCHAR(4),
			LEVEL3_NAME VARCHAR(256) NOT NULL,
            LEVEL3_ID VARCHAR(4) PRIMARY KEY
        );
    END IF;
END $$;


--Tạo bảng FACT_LCTT_GT
DO $$
BEGIN
    -- Kiểm tra xem bảng FACT_LCTT_GT đã tồn tại hay chưa
    IF NOT EXISTS (
        SELECT 1
        FROM pg_catalog.pg_tables
        WHERE tablename = 'FACT_LCTT_GT'
        AND schemaname = 'public'
    ) THEN
        -- Tạo bảng FACT_LCTT_GT nếu nó không tồn tại
        CREATE TABLE FACT_LCTT_GT (
            COMPANY_ID VARCHAR(4) NOT NULL REFERENCES DIM_COMPANY(COMPANY_ID),
            ID VARCHAR(4) NOT NULL REFERENCES DIM_LCTT_GT(LEVEL3_ID),
            VALUE DECIMAL NOT NULL,
            DATE_ID VARCHAR(10) NOT NULL REFERENCES DIM_DATE(DATE_ID),
            CONSTRAINT FACT_LCTT_GT_PK PRIMARY KEY (COMPANY_ID, ID, DATE_ID)
        );
    END IF;
END $$;
