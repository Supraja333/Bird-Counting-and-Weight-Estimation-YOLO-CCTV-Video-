# Bird-Counting-and-Weight-Estimation-YOLO-CCTV-Video-
Overview
This project implements a prototype system for bird (hen) counting and weight estimation from a fixed-camera poultry CCTV video, as per the provided candidate task.
The system uses YOLO-based object detection and tracking to:
1. Detect birds (hens) in each frame
2. Assign stable tracking IDs to avoid double counting
3. Produce bird counts over time
4. Estimate per-bird and aggregate weight using a relative weight proxy derived from bounding box area.

Key Features
Bird Detection: YOLO pretrained model (COCO bird class)
Tracking: ByteTrack for stable tracking IDs
Counting Logic: Unique track IDs per frame → avoids double counting
Weight Estimation: Bounding-box-area–based relative weight index
Artifacts:
Annotated output video (bounding boxes, IDs, count overlay)
JSON output with counts, tracking data, and weight estimates.

API Specification
GET /health
Returns a simple health check response.
Response:
{"status": "ok"}
POST /analyze_video
Analyzes an uploaded CCTV video.
Request:
Method: POST
Content-Type: multipart/form-data
File field: video
Optional Parameters:
fps_sample: Frame sampling rate
conf_thresh: Detection confidence threshold
iou_thresh: IOU threshold

Response (JSON):
{
"counts": [{"frame": 10, "count": 5}],
"tracks_sample": [
{"track_id": 1, "bbox": [x1,y1,x2,y2]}
],
"weight_estimates": [
{"track_id": 1, "weight_index": 2.35}
],
"artifacts": {
"annotated_video": "annotated_hen_detection.mp4",
"json_output": "hen_count_weight.json"
}
}
