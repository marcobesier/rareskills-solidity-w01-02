# Why does the SafeERC20 program exist and when should it be used?

SafeERC20 is a library that provides a set of wrappers around ERC20 operations to safely call ERC20 token functions. The need for such a library arose because not all ERC20 tokens adhere to the standard perfectly. Some tokens have inconsistencies or non-standard behavior, leading to issues when interacting with them.

## Why SafeERC20 exists

1. **Return values inconsistency:** The standard ERC20 interface requires `transfer`, `transferFrom`, and `approve` to return a boolean indicating success or failure. In practice, however, there are many token contracts that don't return anything. SafeERC20 supports such tokens as well by explicitly creating the correct return value (`false` if the call reverts or throws on failure, `true` if the call doesn't revert).

2. **Approve double-spend problem:** Calling `approve` on an ERC20 token with a non-zero allowance [can be risky](https://docs.google.com/document/d/1YLPtQxZu1UAvO9cZ1O2RPXBbT0mooh4DYKjA_jp-RLM/edit#heading=h.m9fhqynw2xvt). SafeERC20 provides methods to safely set the allowance to zero before setting a new allowance, mitigating potential double-spend problems.

## When should you use SafeERC20

If your contract is meant to interact with arbitrary ERC20 tokens, using SafeERC20 can guard against potential inconsistencies with the original specification and mitigate the risk of double-spending an allowance.

## Conclusion

In summary, SafeERC20 exists to handle inconsistencies and potential pitfalls when interacting with ERC20 tokens. If you're developing a contract that interacts with ERC20 tokens, especially in a generic manner, it's a good idea to consider using SafeERC20 to ensure safe and consistent behavior.
