# Specification: Refund Calculation Logic

## 1. Overview
This document defines the requirements for the refund service.

## 2. Mathematical Formula
All partial refunds must follow the proportional tax rule:

$$Tax_{refund} = \left( \frac{Amount_{refund}}{Amount_{total}} \right) \times Tax_{total}$$

## 3. Technical Constraints
* **Data Types:** Use `Decimal` for all currency calculations to ensure 100% accuracy (no floating-point errors).
* **Rounding:** Results must be rounded to exactly **2 decimal places** using the **HALF_UP** method.
* **Input Validation:** * $Amount_{refund} > 0$
    * $Amount_{refund} \leq Amount_{total}$

## 4. Expected API Behavior
* **Endpoint:** `POST /refund`
* **Content-Type:** `application/json`
* **Success Response:** `200 OK` with JSON body `{"tax_refund": "X.XX"}`