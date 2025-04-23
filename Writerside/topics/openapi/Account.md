# Account

The Account resource represents a bank account within the system. It contains
essential information such as the account holder’s details, balance, and
account type. This resource is used for managing individual bank accounts and
their associated transactions.

The balance of an account may only be changed via deposits and withdrawals. The
property is read-only. For savings accounts, the balance must be positive or
zero at all times. A current account can hold a negative balance when the
account has an overdraft limit set.

<api-schema openapi-path="../../../openapi.yml" name="Account"/>
