Question 1:
--rm

Question 2:
0.42.0

Question 3:
SELECT COUNT(*)
FROM green_taxi_trips as gt
WHERE DATE(gt."lpep_pickup_datetime") = '2019-09-18';

Answer:
15767

Question 4:
SELECT DATE(lpep_pickup_datetime) as pt, max(trip_distance) mt
FROM green_taxi_trips
GROUP BY pt
ORDER BY mt DESC;

Answer:
2019-09-26

Question 5:
SELECT gz."Borough" AS pickup_borough,
       SUM(gt.total_amount) AS total_amount_sum
FROM green_taxi_trips gt
JOIN green_taxi_zones gz ON gt."PULocationID" = gz."LocationID"
WHERE DATE(gt."lpep_pickup_datetime") = '2019-09-18'
GROUP BY pickup_borough
HAVING SUM(gt.total_amount) > 50000
ORDER BY total_amount_sum DESC;

Answer:
"Brooklyn" "Manhattan" "Queens"

Question 6:
SELECT gz_dropoff."Zone" AS dropoff_zone_name,
       MAX(gt.tip_amount) AS largest_tip_amount
FROM green_taxi_trips gt
JOIN green_taxi_zones gz_pickup ON gt."PULocationID" = gz_pickup."LocationID"
JOIN green_taxi_zones gz_dropoff ON gt."DOLocationID" = gz_dropoff."LocationID"
WHERE DATE(gt."lpep_pickup_datetime") >= '2019-09-01'
  AND DATE(gt."lpep_pickup_datetime") <= '2019-09-30'
  AND gz_pickup."Zone" = 'Astoria'
GROUP BY dropoff_zone_name
ORDER BY largest_tip_amount DESC
LIMIT 1;

Answer:
JFK Airport

Question 7:

Terraform used the selected providers to generate the following execution plan. Resource
actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # google_bigquery_dataset.demo_dataset will be created
  + resource "google_bigquery_dataset" "demo_dataset" {
      + creation_time              = (known after apply)
      + dataset_id                 = "ny_taxi"
      + default_collation          = (known after apply)
      + delete_contents_on_destroy = false
      + effective_labels           = (known after apply)
      + etag                       = (known after apply)
      + id                         = (known after apply)
      + is_case_insensitive        = (known after apply)
      + last_modified_time         = (known after apply)
      + location                   = "us-central1"
      + max_time_travel_hours      = (known after apply)
      + project                    = "argon-tuner-410118"
      + self_link                  = (known after apply)
      + storage_billing_model      = (known after apply)
      + terraform_labels           = (known after apply)
    }

  # google_storage_bucket.demo-bucket will be created
  + resource "google_storage_bucket" "demo-bucket" {
      + effective_labels            = (known after apply)
      + force_destroy               = true
      + id                          = (known after apply)
      + location                    = "US-CENTRAL1"
      + name                        = "terraform-demo-terra-bucket-argon-tuner-410118"
      + project                     = (known after apply)
      + public_access_prevention    = (known after apply)
      + self_link                   = (known after apply)
      + storage_class               = "STANDARD"
      + terraform_labels            = (known after apply)
      + uniform_bucket_level_access = (known after apply)
      + url                         = (known after apply)

      + lifecycle_rule {
          + action {
              + type = "AbortIncompleteMultipartUpload"
            }
          + condition {
              + age                   = 1
              + matches_prefix        = []
              + matches_storage_class = []
              + matches_suffix        = []
              + with_state            = (known after apply)
            }
        }
    }

Plan: 2 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

google_bigquery_dataset.demo_dataset: Creating...
google_storage_bucket.demo-bucket: Creating...
google_bigquery_dataset.demo_dataset: Creation complete after 1s [id=projects/argon-tuner-410118/datasets/ny_taxi]
google_storage_bucket.demo-bucket: Creation complete after 1s [id=terraform-demo-terra-bucket-argon-tuner-410118]