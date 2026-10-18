# Data

The dataset comes from the internal customer feedback system of House of Travels & Tourism (Pvt) Ltd
and is **confidential**. It is not included in this repository. Use of the data for this research was
approved by the company (see Appendix A of the report).

## Expected structure (to reproduce with your own data)

One row per guest review of one hotel stay.

| Column | Type | Description |
|---|---|---|
| Booking No | text | Booking identifier |
| Hotel | integer | Hotel ID |
| Hotel Name | text | Hotel name (joined from the hotel list) |
| Nationality | text | Guest nationality (joined from booking data) |
| Welcome / Check in | ordinal | UNACCEPTABLE, POOR, SATISFACTORY, GOOD, EXCELLENT |
| Standard of the room | ordinal | same scale |
| Cleanliness | ordinal | same scale |
| Restaurant Service | ordinal | same scale |
| Quality Meals | ordinal | same scale |
| Attentiveness / Friendliness of Hotel staffs | ordinal | same scale |
| Overall Rating | ordinal | same scale |

Ratings are encoded 0 to 4 in the notebook. The six service features (not Overall Rating) are used for clustering.
