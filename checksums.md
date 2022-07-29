What are checksums and what are they useful for?

- Checksums are "data blocks" generated from the input data that undergo an algorithmic manipulation. 
- They are used to verify data integrity between source and destination since transmission errors may be introduced.
- Knowing the checksum produced from the source let's us verify the accuracy of the data received by the destination. 
- If the destination data produces the same checksum, data is correct.
- Examples: I have used CRCs in the BLE "paring ID" and a CRC is run on the firmware image.
