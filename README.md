# bank-management
banking-management-3-module

Banking System:

project documentation:

I have used below things in my project
- pagination
- api-documentation
- exception-handling - global exception handler
- Bean Validation
- create user defined exception
- dto
- mapper
- Response Entity
- account number SBI + 15 Digit unique generation
------------------------------------------------------------------------------

Account API : 

1.GET ALL ACCOUNT DETAILS: (pagination use pannirukan)

Type: Get
http://localhost:8080/accounts?page_no=0&size=10

output:

{
    "content": [
        {
            "accNumber": "SBI356486223444794",
            "name": "surya",
            "balance": 2000.0
        },
        {
            "accNumber": "SBI427988393077775",
            "name": "sharath",
            "balance": 11800.0
        },
        {
            "accNumber": "SBI612321987259380",
            "name": "suku",
            "balance": 2000.0
        },
        {
            "accNumber": "SBI764375038566734",
            "name": "logesh",
            "balance": 6500.0
        },
        {
            "accNumber": "SBI815113054634480",
            "name": "sridharan",
            "balance": 2800.0
        },
        {
            "accNumber": "SBI839837738450934",
            "name": "bharath",
            "balance": 1000.0
        }
    ],
    "empty": false,
    "first": true,
    "last": true,
    "number": 0,
    "numberOfElements": 6,
    "pageable": {
        "offset": 0,
        "pageNumber": 0,
        "pageSize": 10,
        "paged": true,
        "sort": {
            "empty": true,
            "sorted": false,
            "unsorted": true
        },
        "unpaged": false
    },
    "size": 10,
    "sort": {
        "empty": true,
        "sorted": false,
        "unsorted": true
    },
    "totalElements": 6,
    "totalPages": 1
}

2. Get a specific account detail using account Number

Type : Get
http://localhost:8080/account/SBI764375038566734

output:

{
    "accNumber": "SBI764375038566734",
    "name": "logesh",
    "balance": 6500.0
}


3. create a account:

Type:Post

http://localhost:8080/account

Request Body:

{
    
    "name": "ashwin",
    "balance": 16500.0
}



Output:

{
    "accNumber": "SBI220425821763779",
    "name": "ashwin",
    "balance": 16500.0
}


4. update a account

Type : Update - (update apdinaaley full update dhaan) - partial update venumna patch use pannikalam 

http://localhost:8080/account/SBI612321987259380

Request Body:

{
    "name": "sukumar",
    "balance" : 5600
    
}

output:

{
    "accNumber": "SBI612321987259380",
    "name": "sukumar",
    "balance": 5600.0
}




5. delete an account

Type: Delete

http://localhost:8080/account/SBI220425821763779


output:

Account deleted successfully

------------------------------------------------------------------------------

Transaction API:

1. Deposit API:

Type:post 

http://localhost:8080/account/SBI356486223444794/deposit?amount=7800

output:

7800.0 is deposited successfully, and the balance is 9800.0

2. Withdraw API:

Type:post 

http://localhost:8080/account/SBI356486223444794/withdraw?amount=7800

output:

7800.0 is withdraw successfully, and the balance is 2000.0

3. Transfer API:

TYPE : post

http://localhost:8080/transfer?fromId=SBI764375038566734&toId=SBI815113054634480&amount=350

output:

Transfer successful

------------------------------------------------------------------------------

//here we use filter: thats why we use jpa named query:

1. select * from transaction_history where accNum = "SBI427988393077775";

JPA derived query method: List<TransactionHistory>  findByAccount_AccNumber(String accNum,Pageable pageable); 
- also inga pagination use pannirukom

- find By na search 
- Account is a field is present in my Transction History.
- _ underscore is a inside account field -> nested object
- AccNumber - accNumber field is present in account object .
- get accnumber from there idhan inga nadakuthu

2. select * from transaction_history where accNum = "SBI427988393077775" and type = "deposit";
   select * from transaction_history where accNum = "SBI427988393077775" and type = "withdraw";
   select * from transaction_history where accNum = "SBI427988393077775" and type = "transfer";

JPA derived query method: findByAccount_AccNumberAndType(String accNum,Pageable pageable);

same its like above also add Type field in Transactionistory table:


Transaction History API:

1. Get  all transaction list for an account using accNumber also use pagination

http://localhost:8080/account/SBI427988393077775/transactions?page_no=0&size=10

output:

{
    "content": [
        {
            "id": 9,
            "type": "TRANSFER",
            "amount": 2000.0,
            "date": "2026-04-05T02:39:24.267713",
            "message": "Transferred 2000.0 to logesh",
            "account": {
                "accNumber": "SBI427988393077775",
                "name": "sharath",
                "balance": 11800.0
            }
        },
        {
            "id": 11,
            "type": "WITHDRAW",
            "amount": 2000.0,
            "date": "2026-04-05T02:40:54.81283",
            "message": "Amount withdraw successfully",
            "account": {
                "accNumber": "SBI427988393077775",
                "name": "sharath",
                "balance": 11800.0
            }
        },
        {
            "id": 12,
            "type": "DEPOSIT",
            "amount": 7800.0,
            "date": "2026-04-05T02:41:13.732171",
            "message": "Amount deposited successfully",
            "account": {
                "accNumber": "SBI427988393077775",
                "name": "sharath",
                "balance": 11800.0
            }
        }
    ],
    "empty": false,
    "first": true,
    "last": true,
    "number": 0,
    "numberOfElements": 3,
    "pageable": {
        "offset": 0,
        "pageNumber": 0,
        "pageSize": 10,
        "paged": true,
        "sort": {
            "empty": true,
            "sorted": false,
            "unsorted": true
        },
        "unpaged": false
    },
    "size": 10,
    "sort": {
        "empty": true,
        "sorted": false,
        "unsorted": true
    },
    "totalElements": 3,
    "totalPages": 1
}


2.  Get  depost transaction list only for an account using accNumber also use pagination:


Type: Get

http://localhost:8080/account/SBI427988393077775/transactions/deposit?page_no=0&size=10


output:
{
    "content": [
        {
            "id": 12,
            "type": "DEPOSIT",
            "amount": 7800.0,
            "date": "2026-04-05T02:41:13.732171",
            "message": "Amount deposited successfully",
            "account": {
                "accNumber": "SBI427988393077775",
                "name": "sharath",
                "balance": 11800.0
            }
        }
    ],
    "empty": false,
    "first": true,
    "last": true,
    "number": 0,
    "numberOfElements": 1,
    "pageable": {
        "offset": 0,
        "pageNumber": 0,
        "pageSize": 10,
        "paged": true,
        "sort": {
            "empty": true,
            "sorted": false,
            "unsorted": true
        },
        "unpaged": false
    },
    "size": 10,
    "sort": {
        "empty": true,
        "sorted": false,
        "unsorted": true
    },
    "totalElements": 1,
    "totalPages": 1
}


3. Get  withdraw transaction list only for an account using accNumber also use pagination


Type : Get

http://localhost:8080/account/SBI427988393077775/transactions/withdraw?page_no=0&size=10

output:

{
    "content": [
        {
            "id": 11,
            "type": "WITHDRAW",
            "amount": 2000.0,
            "date": "2026-04-05T02:40:54.81283",
            "message": "Amount withdraw successfully",
            "account": {
                "accNumber": "SBI427988393077775",
                "name": "sharath",
                "balance": 11800.0
            }
        }
    ],
    "empty": false,
    "first": true,
    "last": true,
    "number": 0,
    "numberOfElements": 1,
    "pageable": {
        "offset": 0,
        "pageNumber": 0,
        "pageSize": 10,
        "paged": true,
        "sort": {
            "empty": true,
            "sorted": false,
            "unsorted": true
        },
        "unpaged": false
    },
    "size": 10,
    "sort": {
        "empty": true,
        "sorted": false,
        "unsorted": true
    },
    "totalElements": 1,
    "totalPages": 1
}

4.  Get  transfer transaction list only for an account using accNumber also use pagination:

Type : Get

http://localhost:8080/account/SBI427988393077775/transactions/transfer?page_no=0&size=10

Output:

{
    "content": [
        {
            "id": 9,
            "type": "TRANSFER",
            "amount": 2000.0,
            "date": "2026-04-05T02:39:24.267713",
            "message": "Transferred 2000.0 to logesh",
            "account": {
                "accNumber": "SBI427988393077775",
                "name": "sharath",
                "balance": 11800.0
            }
        }
    ],
    "empty": false,
    "first": true,
    "last": true,
    "number": 0,
    "numberOfElements": 1,
    "pageable": {
        "offset": 0,
        "pageNumber": 0,
        "pageSize": 10,
        "paged": true,
        "sort": {
            "empty": true,
            "sorted": false,
            "unsorted": true
        },
        "unpaged": false
    },
    "size": 10,
    "sort": {
        "empty": true,
        "sorted": false,
        "unsorted": true
    },
    "totalElements": 1,
    "totalPages": 1
}



--------------------------------------------------------------------------

Mini Project 

SBI Banking System:

project documentation:

I have used below things in my project
- pagination
- api-documentation
- exception-handling - global exception handler
- Bean Validation
- create user defined exception
- dto
- mapper
- account number SBI + 15 Digit unique generate pannirukan
------------------------------------------------------------------------------

Account API : 

1.GET ALL ACCOUNT DETAILS: (pagination use pannirukan)

Type: Get
http://localhost:8080/accounts?page_no=0&size=10

output:

{
    "content": [
        {
            "accNumber": "SBI356486223444794",
            "name": "surya",
            "balance": 2000.0
        },
        {
            "accNumber": "SBI427988393077775",
            "name": "sharath",
            "balance": 11800.0
        },
        {
            "accNumber": "SBI612321987259380",
            "name": "suku",
            "balance": 2000.0
        },
        {
            "accNumber": "SBI764375038566734",
            "name": "logesh",
            "balance": 6500.0
        },
        {
            "accNumber": "SBI815113054634480",
            "name": "sridharan",
            "balance": 2800.0
        },
        {
            "accNumber": "SBI839837738450934",
            "name": "bharath",
            "balance": 1000.0
        }
    ],
    "empty": false,
    "first": true,
    "last": true,
    "number": 0,
    "numberOfElements": 6,
    "pageable": {
        "offset": 0,
        "pageNumber": 0,
        "pageSize": 10,
        "paged": true,
        "sort": {
            "empty": true,
            "sorted": false,
            "unsorted": true
        },
        "unpaged": false
    },
    "size": 10,
    "sort": {
        "empty": true,
        "sorted": false,
        "unsorted": true
    },
    "totalElements": 6,
    "totalPages": 1
}

2. Get a specific account detail using account Number

Type : Get
http://localhost:8080/account/SBI764375038566734

output:

{
    "accNumber": "SBI764375038566734",
    "name": "logesh",
    "balance": 6500.0
}


3. create a account:

Type:Post

http://localhost:8080/account

Request Body:

{
    
    "name": "ashwin",
    "balance": 16500.0
}



Output:

{
    "accNumber": "SBI220425821763779",
    "name": "ashwin",
    "balance": 16500.0
}


4. update a account

Type : Update - (update apdinaaley full update dhaan) - partial update venumna patch use pannikalam 

http://localhost:8080/account/SBI612321987259380

Request Body:

{
    "name": "sukumar",
    "balance" : 5600
    
}

output:

{
    "accNumber": "SBI612321987259380",
    "name": "sukumar",
    "balance": 5600.0
}




5. delete an account

Type: Delete

http://localhost:8080/account/SBI220425821763779


output:

Account deleted successfully

------------------------------------------------------------------------------

Transaction API:

1. Deposit API:

Type:post 

http://localhost:8080/account/SBI356486223444794/deposit?amount=7800

output:

7800.0 is deposited successfully, and the balance is 9800.0

2. Withdraw API:

Type:post 

http://localhost:8080/account/SBI356486223444794/withdraw?amount=7800

output:

7800.0 is withdraw successfully, and the balance is 2000.0

3. Transfer API:

TYPE : post

http://localhost:8080/transfer?fromId=SBI764375038566734&toId=SBI815113054634480&amount=350

output:

Transfer successful

------------------------------------------------------------------------------

//here we use filter: thats why we use jpa named query:

1. select * from transaction_history where accNum = "SBI427988393077775";

JPA derived query method: List<TransactionHistory>  findByAccount_AccNumber(String accNum,Pageable pageable); 
- also inga pagination use pannirukom

- find By na search 
- Account is a field is present in my Transction History.
- _ underscore is a inside account field -> nested object
- AccNumber - accNumber field is present in account object .
- get accnumber from there idhan inga nadakuthu

2. select * from transaction_history where accNum = "SBI427988393077775" and type = "deposit";
   select * from transaction_history where accNum = "SBI427988393077775" and type = "withdraw";
   select * from transaction_history where accNum = "SBI427988393077775" and type = "transfer";

JPA derived query method: findByAccount_AccNumberAndType(String accNum,Pageable pageable);

same its like above also add Type field in Transactionistory table:


Transaction History API:

1. Get  all transaction list for an account using accNumber also use pagination

http://localhost:8080/account/SBI427988393077775/transactions?page_no=0&size=10

output:

{
    "content": [
        {
            "id": 9,
            "type": "TRANSFER",
            "amount": 2000.0,
            "date": "2026-04-05T02:39:24.267713",
            "message": "Transferred 2000.0 to logesh",
            "account": {
                "accNumber": "SBI427988393077775",
                "name": "sharath",
                "balance": 11800.0
            }
        },
        {
            "id": 11,
            "type": "WITHDRAW",
            "amount": 2000.0,
            "date": "2026-04-05T02:40:54.81283",
            "message": "Amount withdraw successfully",
            "account": {
                "accNumber": "SBI427988393077775",
                "name": "sharath",
                "balance": 11800.0
            }
        },
        {
            "id": 12,
            "type": "DEPOSIT",
            "amount": 7800.0,
            "date": "2026-04-05T02:41:13.732171",
            "message": "Amount deposited successfully",
            "account": {
                "accNumber": "SBI427988393077775",
                "name": "sharath",
                "balance": 11800.0
            }
        }
    ],
    "empty": false,
    "first": true,
    "last": true,
    "number": 0,
    "numberOfElements": 3,
    "pageable": {
        "offset": 0,
        "pageNumber": 0,
        "pageSize": 10,
        "paged": true,
        "sort": {
            "empty": true,
            "sorted": false,
            "unsorted": true
        },
        "unpaged": false
    },
    "size": 10,
    "sort": {
        "empty": true,
        "sorted": false,
        "unsorted": true
    },
    "totalElements": 3,
    "totalPages": 1
}


2.  Get  depost transaction list only for an account using accNumber also use pagination:


Type: Get

http://localhost:8080/account/SBI427988393077775/transactions/deposit?page_no=0&size=10


output:
{
    "content": [
        {
            "id": 12,
            "type": "DEPOSIT",
            "amount": 7800.0,
            "date": "2026-04-05T02:41:13.732171",
            "message": "Amount deposited successfully",
            "account": {
                "accNumber": "SBI427988393077775",
                "name": "sharath",
                "balance": 11800.0
            }
        }
    ],
    "empty": false,
    "first": true,
    "last": true,
    "number": 0,
    "numberOfElements": 1,
    "pageable": {
        "offset": 0,
        "pageNumber": 0,
        "pageSize": 10,
        "paged": true,
        "sort": {
            "empty": true,
            "sorted": false,
            "unsorted": true
        },
        "unpaged": false
    },
    "size": 10,
    "sort": {
        "empty": true,
        "sorted": false,
        "unsorted": true
    },
    "totalElements": 1,
    "totalPages": 1
}


3. Get  withdraw transaction list only for an account using accNumber also use pagination


Type : Get

http://localhost:8080/account/SBI427988393077775/transactions/withdraw?page_no=0&size=10

output:

{
    "content": [
        {
            "id": 11,
            "type": "WITHDRAW",
            "amount": 2000.0,
            "date": "2026-04-05T02:40:54.81283",
            "message": "Amount withdraw successfully",
            "account": {
                "accNumber": "SBI427988393077775",
                "name": "sharath",
                "balance": 11800.0
            }
        }
    ],
    "empty": false,
    "first": true,
    "last": true,
    "number": 0,
    "numberOfElements": 1,
    "pageable": {
        "offset": 0,
        "pageNumber": 0,
        "pageSize": 10,
        "paged": true,
        "sort": {
            "empty": true,
            "sorted": false,
            "unsorted": true
        },
        "unpaged": false
    },
    "size": 10,
    "sort": {
        "empty": true,
        "sorted": false,
        "unsorted": true
    },
    "totalElements": 1,
    "totalPages": 1
}

4.  Get  transfer transaction list only for an account using accNumber also use pagination:

Type : Get

http://localhost:8080/account/SBI427988393077775/transactions/transfer?page_no=0&size=10

Output:

{
    "content": [
        {
            "id": 9,
            "type": "TRANSFER",
            "amount": 2000.0,
            "date": "2026-04-05T02:39:24.267713",
            "message": "Transferred 2000.0 to logesh",
            "account": {
                "accNumber": "SBI427988393077775",
                "name": "sharath",
                "balance": 11800.0
            }
        }
    ],
    "empty": false,
    "first": true,
    "last": true,
    "number": 0,
    "numberOfElements": 1,
    "pageable": {
        "offset": 0,
        "pageNumber": 0,
        "pageSize": 10,
        "paged": true,
        "sort": {
            "empty": true,
            "sorted": false,
            "unsorted": true
        },
        "unpaged": false
    },
    "size": 10,
    "sort": {
        "empty": true,
        "sorted": false,
        "unsorted": true
    },
    "totalElements": 1,
    "totalPages": 1
}



--------------------------------------------------------------------------





 
