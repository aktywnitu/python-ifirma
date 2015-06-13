python-ifirma (in progress)
======

Extremely simple wrapper for iFirma API.

##Features

**Implemented**

- generating invoice in iFirma service

**Very soon**

- downloading invoice PDF
- generating proforma invoice
- generating invoice based on proforma

##Prerequisites

Go to your iFirma account and generate API keys of following types:

- *faktura* (required)
- *abonent* (optional)


**Testing**

iFirma offers [demo account](https://www.ifirma.pl/cgi-bin/WebObjects/ifirma-demo.woa/wa/demo) that can be used for testing and development

##Installation

Just add following line to your `requirements.txt` and let `pip` do rest of the work
```
-e -e git+git://github.com/DariuszAniszewski/python-ifirma.git#egg=python-ifirma
```

##Usage

#####1. Create instance of iFirmaAPI
```python
ifirma_client = iFirmaAPI(TEST_IFIRMA_USER, TEST_IFIRMA_INVOICE_KEY, TEST_IFIRMA_USER_KEY)
```
#####2. Create invoice parameters
```python
client = Client(
    "Dariusz Aniszewski's Company",  # company name
    "PL1231231212",  # Tax ID
    Address(
        "Otwock",  # City
        "00-000"  # Zip code
    ),
    email="email@server.com",
)

position = Position(
    VAT.VAT_23,  # VAT rate 
    1,  # Quantity
    1000,  # Unit price
    "nazwa",  # Position name
    "szt"  # Position unit
)
```

#####3. Create invoice in iFirma service and get it's id
```python
invoice = NewInvoiceParams(client, [position])
invoice_id = ifirma_client.generate_invoice(invoice)
```

In near future you can use `invoice_id` to perform other actions like downloading PDF or getting details.

**That's all folks**
