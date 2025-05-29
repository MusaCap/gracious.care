# Data Model – Personal AI Healthcare Advocate

## Entity: User
- `user_id` (UUID): Unique identifier
- `name` (String)
- `email` (String)
- `phone_number` (String, optional)
- `preferred_language` (String)
- `timezone` (String)
- `demographics` (Object)
  - `ethnicity` (String)
  - `gender_identity` (String)
  - `age_range` (String)
- `health_goals` (Array[String])
- `privacy_settings` (Object)
  - `data_sharing_opt_in` (Boolean)
  - `recording_opt_in` (Boolean)
- `trusted_contacts` (Array[UserReference])

## Entity: UserReference
- `name` (String)
- `relationship` (String)
- `contact_email` (String)

## Entity: HealthProfile
- `profile_id` (UUID)
- `user_id` (UUID, FK → User)
- `conditions` (Array[String])
- `medications` (Array[Medication])
- `allergies` (Array[String])
- `insurance_info` (Object)
  - `provider` (String)
  - `policy_number` (String)
- `preferred_providers` (Array[ProviderReference])
- `language_proficiency_level` (Enum: Low, Medium, High)

## Entity: Medication
- `name` (String)
- `dosage` (String)
- `frequency` (String)
- `prescribing_doctor` (ProviderReference)

## Entity: Appointment
- `appointment_id` (UUID)
- `user_id` (UUID, FK → User)
- `provider` (ProviderReference)
- `appointment_type` (String)
- `location` (String)
- `datetime` (Datetime)
- `pre_appointment_notes` (Text)
- `suggested_questions` (Array[String])
- `recording_available` (Boolean)
- `transcript_id` (UUID, FK → Transcript, optional)
- `post_visit_summary_id` (UUID, FK → Summary, optional)

## Entity: Transcript
- `transcript_id` (UUID)
- `appointment_id` (UUID, FK → Appointment)
- `raw_text` (Text)
- `emotion_tags` (Array[String])
- `flagged_terms` (Array[String])
- `timestamped_notes` (Array[Note])

## Entity: Note
- `timestamp` (Datetime)
- `content` (String)
- `highlighted_term` (String, optional)

## Entity: Summary
- `summary_id` (UUID)
- `appointment_id` (UUID, FK → Appointment)
- `summary_text` (Text)
- `next_steps` (Array[String])
- `clarification_needed` (Array[String])
- `medical_terms_explained` (Map[String → String])

## Entity: ProviderReference
- `name` (String)
- `specialty` (String)
- `affiliation` (String)
- `contact_info` (Object)
  - `phone` (String)
  - `email` (String)
  - `address` (String)

## Entity: HealthEducationResource
- `resource_id` (UUID)
- `title` (String)
- `content` (Text or URL)
- `topic` (String)
- `language` (String)
- `literacy_level` (Enum: Basic, Intermediate, Advanced)
- `recommended_for` (Array[Condition])

## Entity: Condition
- `condition_id` (UUID)
- `name` (String)
- `description` (Text)
- `related_medications` (Array[String])
- `common_questions` (Array[String])
- `minority_specific_considerations` (Text)

## Entity: AdvocacyLog
- `log_id` (UUID)
- `user_id` (UUID)
- `timestamp` (Datetime)
- `issue_reported` (String)
- `action_taken` (String)
- `escalated_to_navigator` (Boolean)
