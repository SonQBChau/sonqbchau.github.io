---
layout: ../../layouts/BlogLayout.astro
title: Mockaroo tips and tricks
published: 'Aug 22 2024'
tags: [mock]
---

[Mockaroo](https://www.mockaroo.com) comes with an intuitive interface to generate data. For example, to create an email address, we can put an email into the `Field Name`, select `Email Address` from `Type`, then choose how many rows we want to generate.

Most of the `Types` are self-explanatory and come with examples. Some of the slightly advanced use cases for data generation are below:

### Use Hidden Field

Put a double underscore in front of the **Field Name** to prevent it from showing (but it can still be referenced).
<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img width="622" alt="hidden_field" src="https://github.com/user-attachments/assets/1350c861-18bf-49b9-af1a-4a771b242f7f">
</figure>

### Use Reference Field

Use the **Template** type and curly brackets for reference.

For example, if we want to generate `PROGRAM_1`, `PROGRAM_2`, `PROGRAM_3`…

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img width="625" alt="reference_field" src="https://github.com/user-attachments/assets/5c1ac1da-fc13-47c8-80fa-7d4016583389">
</figure>

### Append Value to a Number

Use the formula:

```ruby
"PROGRAM_" + this.to_s
```

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img width="738" alt="value_to_number" src="https://github.com/user-attachments/assets/a8a014db-90bc-47c2-9481-02e47e18abc1">
</figure>

### Use Foreign Key

We can link a field from another table through `Dataset Column`.

For example, if we want to link a `Donor` to the `Program`:

1. Create a `Program` schema, then click `Create Dataset` (small arrow next to the **Download Data** button).
2. Create a `Donor` schema, choose `Dataset Column`, and the field to reference.

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img width="738" alt="foreign_key" src="https://github.com/user-attachments/assets/60ca008d-94e4-413c-a34e-0ab22c2fddb2">
</figure>

### Use Nested Object

Refer to Mockaroo’s docs here: [Mockaroo JSON Help](https://www.mockaroo.com/help/json)

For example, if we want `gender` to contain a list of objects:

```json
"gender": [
  {
    "sex": "Male",
    "count": 303
  },
  {
    "sex": "Female",
    "count": 356
  }
]
```

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img width="738" alt="nested_object" src="https://github.com/user-attachments/assets/63250de1-d130-45af-870e-551a5c5191bf">
</figure>

`gender.sex` Formula

```ruby
if this == 1 then 'Male'
else 'Female' end
```

### Use Custom List

**Method 1**: Use the built-in **Type Custom List**.

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img width="738" alt="custom_list" src="https://github.com/user-attachments/assets/4622a8ea-640e-4721-9486-fd4f56e58485">

</figure>

**Method 2**: Use **Template** and click on the Sigma button at the end.

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img width="738" alt="custom_list_2" src="https://github.com/user-attachments/assets/4e868f29-ce8a-4ffb-a8f3-ed7a6be625e5">
</figure>

Put the name list in the **Formula** area with the random function from 0 to last, for example:

```ruby
[
  "mg/m2",
  "IU/m2",
  "ug/m2",
  "g/m2",
  "mg/kg"
][random(0,4)]
```

### Use Regex

Refer to Mockaroo’s docs: [Mockaroo Regular Expressions Help](https://www.mockaroo.com/help/regular-expressions)

For example, if we want to generate `comorbidity_type_code` like `E10`, `C50.1`, `I11`, `M06`...

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img width="738" alt="regex" src="https://github.com/user-attachments/assets/c1d8b268-d266-4138-9d0a-569f02d17577">

</figure>

### Use Start and End Date

We can create a formula to make sure the end date comes after the start date.

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img width="738" alt="start_end_date" src="https://github.com/user-attachments/assets/4b8214d6-5560-4687-9956-fe72b9963350">

</figure>

In the **Formula** (Sigma button), put in:

```ruby
birth_year = year(date_of_birth)
curr_year = year(now())
life_span = curr_year - birth_year
date_of_birth + years(random(1, life_span))
```

### Use Random Number

The **Number Type** is random by default, just give it a range (min-max) and it will generate a random number.

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img width="738" alt="start_end_date" src="https://github.com/user-attachments/assets/9f357c20-d77c-484d-88f6-b89d93540607">

</figure>

### Use Condition to Show Value

Use the **Formula** (Sigma button) to check for an `if` condition, then put the value after `then`.

For example, if we want to show `date_of_death` only if `is_deceased` is true:

<figure style="margin-bottom: 1em; margin-top: 1em;">
  <img width="738" alt="start_end_date" src="https://github.com/user-attachments/assets/f4a1616c-4293-4842-a521-2fcfc746cb18">

</figure>

Inside the `date_of_death` formula:

```ruby
birth_year = year(date_of_birth)
curr_year = year(now())
life_span = curr_year - birth_year
death_year = date_of_birth + years(random(1, life_span))

if is_deceased == true
then death_year
else nil end
```

Another example, if we want to show `date_of_birth.day_interval` based on the condition of `date_resolution`:

```ruby
if date_resolution == 'day' && !field('date_of_birth.month_interval').nil?
then field('date_of_birth.month_interval') * 30
else nil end
```

These tips should help you get more out of Mockaroo. Explore the options and see how they fit into your projects!