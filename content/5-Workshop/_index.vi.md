---
title: "Workshop FCAJ Hybrid SOC/AWS"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---


## Tổng quan

Workshop này mô tả project FCAJ Hybrid SOC/AWS: một pipeline SOC hybrid bắt đầu từ security evidence ở local lab, đưa event lên AWS, xử lý qua các cloud data service và AI/Fusion component, rồi chuẩn bị final alert cho lưu trữ, monitoring và dashboard downstream.

Workshop hiện được tổ chức thành 11 section chính. Một số section đã có nội dung và evidence, các section còn lại là skeleton placeholder chờ người phụ trách bổ sung nội dung và screenshot đã xác minh.

## Nội dung workshop

1. [Overview and Architecture](5.1-Overview-and-Architecture/)
2. [Prerequisites and Naming](5.2-Prerequisites-and-Naming/)
3. [Networking, IAM and Security Baseline](5.3-Networking-IAM-Security-Baseline/)
4. [Frontend S3, CloudFront and WAF](5.4-Frontend-S3-CloudFront-WAF/)
5. [Backend EC2 Runtime](5.5-Backend-EC2-Runtime/)
6. [SQS, DLQ and S3 Data Bucket](5.6-SQS-DLQ-and-S3-Data-Bucket/)
7. [RDS, Secrets and Worker Pipeline](5.7-RDS-Secrets-Worker-Pipeline/)
8. [AWS Pipeline Validation and Dashboard Evidence](5.8-AWS-Pipeline-Validation-and-Dashboard-Evidence/)
9. [AI Fusion and Dashboard Validation](5.9-AI-Fusion-and-Dashboard-Validation/)
10. [Monitoring, Audit and Notification](5.10-Monitoring-Audit-Notification/)
11. [Cleanup and Cost Control](5.11-Cleanup-and-Cost-Control/)

## Nguyên tắc evidence

Chỉ đưa evidence đã xác minh và đã redact vào workshop. Section nào chưa có evidence phải giữ dạng placeholder và không claim đã triển khai AWS hoàn tất, notification hoạt động, dashboard đã validate thật hoặc production integration.
