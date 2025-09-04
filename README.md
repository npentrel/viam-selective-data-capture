# Selective Image Capture - `imagefilter` modular component

This module implements the [Viam camera API](https://docs.viam.com/dev/reference/apis/components/camera/) in a `viam-soleng:camera:imagefilter` model.
With this model, you can selectively capture and upload images based on vision service detection results. The component filters images before storing and uploading them to the Viam cloud by checking if a vision service detects any objects in the image.

Navigate to the **CONFIGURE** tab of your machine's page.
Click the **+** button, select **Component or service**, then select the `camera / imagefilter` model provided by the [`image_filter` module](https://app.viam.com/module/viam-soleng/image_filter).
Click **Add module**, enter a name for your camera, and click **Create**.

## Configure your `imagefilter` camera

1. On the new component panel, copy and paste the following attribute template into your camera's **Attributes** box:

   ```json
   {
     "vision_service": "<vision_service_name>",
     "actual_cam": "<camera_name>"
   }
   ```

2. Then add the camera and vision service to the **Depend on** section.
3. Finally, configure data capture for the component.

### Attributes

The following attributes are available for `viam-soleng:camera:imagefilter` cameras:

| Name             | Type   | Inclusion | Description                                    |
| ---------------- | ------ | --------- | ---------------------------------------------- |
| `vision_service` | string | **Required**  | Name of the vision service to use for detection |
| `actual_cam`     | string | **Required**  | Name of the actual camera component to capture from |

### Example Configuration

```json
{
  "model": "viam-soleng:camera:imagefilter",
  "type": "camera",
  "namespace": "rdk",
  "attributes": {
    "vision_service": "colordetector",
    "actual_cam": "camera"
  },
  "depends_on": [
    "camera",
    "colordetector"
  ],
  "service_configs": [
    {
      "type": "data_manager",
      "attributes": {
        "capture_methods": [
          {
            "disabled": false,
            "method": "ReadImage",
            "additional_params": {
              "mime_type": "image/jpeg"
            },
            "capture_frequency_hz": 1
          }
        ]
      }
    }
  ],
  "name": "imagefilter"
}
```
