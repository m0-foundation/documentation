# Sherlock Contest Documentation
```
   $$\           $$$$$$\  $$\                 $$\       $$\                                              $$\    
 $$$$$$\        $$  __$$\ \__|                $$ |      $$ |                                           $$$$$$\  
$$  __$$\       $$ /  \__|$$\ $$$$$$$\   $$$$$$$ |      $$$$$$$\  $$\   $$\  $$$$$$\   $$$$$$$\       $$  __$$\ 
$$ /  \__|      $$$$\     $$ |$$  __$$\ $$  __$$ |      $$  __$$\ $$ |  $$ |$$  __$$\ $$  _____|      $$ /  \__|
\$$$$$$\        $$  _|    $$ |$$ |  $$ |$$ /  $$ |      $$ |  $$ |$$ |  $$ |$$ /  $$ |\$$$$$$\        \$$$$$$\  
 \___ $$\       $$ |      $$ |$$ |  $$ |$$ |  $$ |      $$ |  $$ |$$ |  $$ |$$ |  $$ | \____$$\        \___ $$\ 
$$\  \$$ |      $$ |      $$ |$$ |  $$ |\$$$$$$$ |      $$$$$$$  |\$$$$$$  |\$$$$$$$ |$$$$$$$  |      $$\  \$$ |
\$$$$$$  |      \__|      \__|\__|  \__| \_______|      \_______/  \______/  \____$$ |\_______/       \$$$$$$  |
 \_$$  _/                                                                   $$\   $$ |                 \_$$  _/ 
   \ _/                                                                     \$$$$$$  |                   \ _/   
```      
## Code Documentation

### Common

Common contracts and libraries used across the various M^0 Solidity projects.

Repository: https://github.com/MZero-Labs/common

Documentation: [Common Documentation](./docs/common/src/SUMMARY.md)

### Protocol

M^0 is an EVM-compatible, immutable protocol that enables minting and burning of the ERC20 token $M. It also allows for $M distributions to yield earners and governance token ($ZERO) holders. There are three main types of actors in the protocol - Minters, Validators, and Yield Earners - all of which are permissioned via governance. Protocol variables are also managed by governance and are stored in a Registrar configuration contract.

Repository: https://github.com/MZero-Labs/protocol

Engineering spec: [Protocol engineering spec](eng-specs/M%5E0%20Protocol%20Engineering%20Spec_v1.1.pdf)

Documentation: [Protocol Documentation](./docs/protocol/src/SUMMARY.md)

### TTG

A TTG, "Two Token Governance" is a governance mechanism that uses token voting to maintain lists and manage communal property. As its name implies, it primarily optimizes for token holder participation. A TTG is primarily used for permissioning actors and should not be used for funding/financing decisions.

Repository: https://github.com/MZero-Labs/ttg

Engineering spec: [TTG engineering spec](eng-specs/M%5E0%20TTG%20Engineering%20Spec_v1.1.pdf)

Documentation: [TTG Documentation](./docs/ttg/src/SUMMARY.md)

## Previous Audits

### Certora

Type of audit: Security Assessment & Formal Verification Report

Dates: 18 January 2024 to 7 March 2024

Report: [Certora Audit report](audit-reports/Certora%20Audit%20report.pdf)

### ChainSecurity

Type of audit: Security Assessment

Dates: 8 January 2024 to 09 February 2024

Report: [ChainSecurity Audit report](audit-reports/ChainSecurity%20Audit%20report.pdf)

### Independent Security Researcher

Type of audit: Security Assessment

Dates: 19 February 2024 to 23 February 2024

Report: [Independent Security Auditor report](audit-reports/Independent%20Security%20Auditor%20Report.md)

### OpenZeppelin

Type of audit: Security Assessment

Dates: 8 January 2024 to 9 February 2024

Report: [OpenZeppelin Audit report](audit-reports/OpenZeppelin%20Audit%20Report.pdf)

### Prototech Labs

Type of audit: Security Assessment & Invariant Test Suite

Dates: 8 January 2024 to 9 February 2024

Report : [Prototech Labs Audit report](audit-reports/Prototech%20Labs%20Audit%20Report.pdf)

### Quantstamp

Type of audit: Security Assessment

Dates: 8 January 2024 to 29 January 2024

Report: [Quantstamp Audit report](audit-reports/Quantstamp%20Audit%20Report.pdf)

Fixes review: [Quantstamp Fixes review](audit-reports/Quantstamp%20External%20Fix%20Review.pdf)

### ThreeSigma

Type of audit: Security Assessment

Dates: 8 January 2024 to 2 February 2024

Report: [ThreeSigma Audit report](audit-reports/ThreeSigma%20Audit%20Report.pdf)
