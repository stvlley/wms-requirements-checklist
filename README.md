# WMS requirements checklist

Fifty questions to ask before you buy or replace a warehouse management system, written for operators rather than vendors. A good requirement does not ask whether the software "supports picking"; it describes what should happen when the warehouse stops following the happy path.

This is the checklist from the article **[WMS Requirements Checklist: 50 Questions to Ask Before You Buy or Replace a Warehouse Management System](https://www.stridetechworks.com/blog/wms-requirements-checklist)** by Stephen Talley, Stride Techworks, Philadelphia. The article adds the acceptance-test format, a weighted scoring model, the demo script vendors should run, red flags, and an FAQ.

- `CHECKLIST.md`: the ten sections and fifty questions, ready to copy into an RFP.
- `scoring.csv`: one row per question with an empty weight and score column for a vendor comparison.

## How to use it

1. Answer the operational-profile questions about your own warehouse first. Requirements that describe your exceptions are worth more than feature lists.
2. Turn every critical answer into an acceptance test the vendor must pass in a demo on your data.
3. Weight the sections by your warehouse's complexity, then score vendors on operational fit, not presentation quality.

## License

Text: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Attribute to Stride Techworks with a link to the article.

## The 50-question WMS requirements checklist

### 1. Operational profile

Before asking what the WMS can do, define the environment it has to survive.

**1. What unit of work actually moves through the building?**  
Eaches, inner packs, cases, pallets, rolls, drums, serial-numbered equipment, catch weight, or some combination?

**2. What are the real daily and peak volumes?**  
Capture receipts, order lines, picks, pallets, shipments, and concurrent users, not only monthly averages.

**3. How many inventory states matter operationally?**  
Available, allocated, damaged, inspection, quarantine, returned, expired, hold, QA release, and customer-specific states may need different behavior.

**4. What operating models must coexist?**  
B2B replenishment, ecommerce each-pick, store fulfillment, wholesale case-pick, manufacturing supply, or 3PL client inventory can impose very different rules.

**5. Which parts of the operation cannot stop during a system problem?**  
Define the workflows that need offline procedures, fallback modes, queues, or rapid recovery.

If these questions are fuzzy, you are not ready to compare vendors.

You are still discovering the operation.

### 2. Receiving and putaway

Receiving is where bad data first becomes warehouse reality.

**6. Can the WMS receive against a PO, ASN, transfer, return, and unexpected receipt?**

**7. What happens when the quantity, SKU, lot, serial, or packaging received does not match the expected record?**

**8. Can receiving capture lot, expiration, serial, condition, and handling-unit information at the point it becomes known?**

**9. Can putaway rules consider capacity, product characteristics, velocity, temperature zone, compatibility, customer ownership, and existing stock?**

**10. Can an operator override a suggested putaway, and does the system record who changed it and why?**

[GS1's logistics-label guidance](https://www.gs1.org/standards/gs1-logistic-label-guideline/1-3) is useful here because real warehouse identification extends beyond a SKU number. It uses the Serial Shipping Container Code, or SSCC, to identify a logistic unit and supports attributes such as GTIN, quantity, lot, serial, and expiration information.

Do not leave label and identifier strategy until hardware setup.

It is part of the data model.

### 3. Inventory control

A WMS is only useful if operators eventually trust what it says is in the building.

**11. At what level can inventory be identified?**  
SKU, owner, lot, serial, pallet, container, location, sublocation, and status may all matter.

**12. Can inventory be moved, split, merged, repacked, and relabeled without losing history?**

**13. What events can automatically trigger a cycle count?**  
Short pick, empty location, abnormal adjustment, repeated variance, or scheduled classification?

**14. Can counting rules differ by SKU, velocity, value, customer, location, or risk?**

**15. Can the system explain an inventory discrepancy through transaction history without requiring someone to reconstruct it from database queries?**

The last question matters more than the dashboard.

When inventory is wrong, somebody has to answer:

**How did we get here?**

If the WMS cannot show that cleanly, every inventory investigation becomes forensic work.

### 4. Replenishment and slotting

A picking location is useful only while it has product in it.

**16. Can replenishment be triggered by minimum quantity, projected demand, released work, or another operational condition?**

**17. Can the WMS distinguish planned replenishment from emergency replenishment created by an active shortage?**

**18. Can reserve stock be prioritized by lot, age, distance, pallet condition, or handling constraints?**

**19. What happens when the preferred reserve location does not contain what the system thinks it contains?**

**20. Can slotting recommendations use actual demand and movement data without forcing the warehouse to accept every recommendation automatically?**

A sophisticated optimization engine does not compensate for untrustworthy location inventory.

Make the vendor demonstrate the failure condition, not only the recommendation screen.

### 5. Picking, packing, and shipping

Picking is usually where the WMS becomes most visible to the workforce.

**21. Which picking methods are supported for your real order profile?**  
Discrete, batch, cluster, zone, wave, waveless, case, pallet, or hybrid.

**22. How does the system prioritize work when customer priority, carrier cutoff, trailer status, and normal release logic conflict?**

**23. What happens after a short pick?**  
Does the WMS silently short the order, redirect the picker, create replenishment, trigger a count, send an exception, or require supervisor action?

**24. Can packout validate item, quantity, container, customer rules, documents, and carrier requirements before shipment confirmation?**

**25. What exactly causes inventory ownership and order status to change when the shipment is confirmed?**

Make the vendor trace one order from allocation through the ERP or OMS afterward.

You want to see the complete transaction chain, not a successful RF screen.

### 6. Exceptions, returns, and traceability

This is where generic checklists are usually weakest.

**26. Can damaged inventory be isolated immediately without creating a fake location or manual spreadsheet?**

**27. Can returned inventory move through configurable disposition states such as inspect, restock, refurbish, quarantine, and scrap?**

**28. Can supervisors see unresolved warehouse exceptions in one queue with owner, age, severity, and required next action?**

**29. Can the system trace product backward and forward across receipts, locations, handling units, lots, and shipments?**

**30. Can a recall or hold isolate only the affected inventory while allowing unrelated inventory to continue moving?**

Traceability is especially important for food operations. The [FDA Food Traceability Rule materials](https://www.fda.gov/food/food-safety-modernization-act-fsma/traceability-lot-code) explain that covered operations must link required Key Data Elements to the relevant traceability lot code. The requirement is not simply “store a lot number”; the relationship between the lot and the receiving, shipping, or transformation event matters.

[GS1's Global Traceability Standard](https://www.gs1.org/standards/gs1-global-traceability-standard/current-standard) describes the same relationship operationally: a warehouse can maintain links between product identification such as GTIN plus batch or lot and pallet-level SSCC identifiers.

If traceability matters to your business, force the demo through a recall.

Do not accept a screenshot of a lot-search page.

### 7. Integrations, data, and automation

Your WMS will not operate alone.

**31. Which system owns each master record?**  
Item, customer, supplier, order, carrier, location, price, inventory, and shipment ownership should be explicit.

**32. Which integrations are synchronous, asynchronous, batch, or file-based, and what business event does each one represent?**

**33. What happens when an upstream or downstream system is unavailable?**  
Queue, retry, reject, duplicate, or silently fail?

**34. Can integration failures be seen and replayed by an authorized operations or IT user without vendor intervention?**

**35. Can the WMS expose the operational events needed by your reporting, automation, and AI layers without direct database hacks?**

“API available” is not a requirement.

The requirement is that the system can exchange the **specific business events** your operation depends on and recover safely when the exchange fails.

This is also why [instrumenting the operation comes before adding agents](/blog/agentic-ai-supply-chain-shop-floor-visibility). Automation cannot make an inventory event more trustworthy than the system that produced it.

### 8. Operator interface, devices, and floor reliability

The system will eventually be judged by someone wearing gloves and trying to clear a task before break.

**36. How many scans or taps does the common task require?**

**37. Can RF, mobile, or browser workflows work on the devices the operation will actually deploy?**

**38. Are prompts understandable without memorizing internal system codes?**

**39. What happens when Wi-Fi drops, a scanner disconnects, or a session expires in the middle of a transaction?**

**40. Can an interrupted task resume safely without losing work, double-posting inventory, or forcing a supervisor to repair the transaction?**

Test these questions on the floor, at the far end of the rack, with the planned device and a real operator.

A desktop demonstration on perfect Wi-Fi is not an RF acceptance test.

### 9. Security, permissions, and operational control

Warehouse permissions should reflect the consequence of the action, not only the screen a user can open.

**41. Can roles separate routine execution, exception approval, configuration, inventory adjustment, and system administration?**

**42. Can sensitive actions require a reason code, second approval, or threshold-based escalation?**

**43. Does the audit trail show the original value, new value, user, device, time, and related business transaction?**

**44. How are temporary labor, shared devices, service accounts, and vendor support access provisioned and removed?**

**45. Can the operation continue safely during planned maintenance, degraded service, and disaster recovery, and has that recovery been tested?**

“Role-based access” is another checkbox that needs a scenario.

Ask the vendor to show exactly how a supervisor can approve a large adjustment without also gaining the ability to change item masters or delete interface history.

### 10. Reporting, implementation, and total cost

The software is only one part of the system you are buying.

**46. Can operational reporting distinguish backlog, active work, blocked work, exceptions, and completed work using transaction-level data?**

**47. What data must be cleansed, mapped, converted, or archived before go-live, and who owns each decision?**

**48. How will the vendor prove configuration, integrations, devices, labels, performance, security, and exception handling before cutover?**

**49. What support model applies during implementation, hypercare, peak season, upgrades, and a production incident?**

**50. What is the five-year total cost, including licensing, implementation, integrations, data conversion, devices, labels, testing, training, travel, support, upgrades, internal labor, and change requests?**

A low subscription price can coexist with an expensive operating model.

If every report, interface replay, workflow change, or permission adjustment requires a paid vendor ticket, include that dependency in the cost, not in the footnotes.
