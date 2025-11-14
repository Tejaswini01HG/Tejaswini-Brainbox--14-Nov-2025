import React, { useRef, useState } from "react";
import html2canvas from "html2canvas";

export default function CertificateGenerator() {
  const [name, setName] = useState("");
  const [eventName, setEventName] = useState("");
  const [date, setDate] = useState("");
  const certRef = useRef();

  const downloadImage = () => {
    html2canvas(certRef.current).then((canvas) => {
      const link = document.createElement("a");
      link.download = "certificate.png";
      link.href = canvas.toDataURL();
      link.click();
    });
  };

  return (
    <div className="main-container">

      {/* Sidebar */}
      <div className="sidebar">
        <h2 className="sidebar-title">Tools</h2>

        <div className="button-group">
          <button className="tool-button">Add Text</button>
          <button className="tool-button">Upload Logo</button>
          <button className="tool-button">Add Signature</button>
          <button className="tool-button">Add Stamp</button>
        </div>
      </div>

      {/* Content Area */}
      <div className="content-area">

        <div className="form-section">
          <h2>Certificate Details</h2>

          <input
            type="text"
            placeholder="Recipient Name"
            value={name}
            onChange={(e) => setName(e.target.value)}
          />

          <input
            type="text"
            placeholder="Event Name"
            value={eventName}
            onChange={(e) => setEventName(e.target.value)}
          />

          <input
            type="text"
            placeholder="Date"
            value={date}
            onChange={(e) => setDate(e.target.value)}
          />
        </div>

        {/* Certificate Preview + Download Button */}
        <div className="certificate-preview">
          <div className="certificate-box" ref={certRef}>
            <h1 className="cert-title">Certificate of Achievement</h1>
            <p className="cert-text">This certificate is proudly presented to:</p>
            <h2 className="cert-name">{name || "Recipient Name"}</h2>
            <p className="cert-event">
              For outstanding achievement<br />
              <b>{eventName || "Event Name"}</b>
            </p>
            <p className="cert-date">Issued on: {date || "DD/MM/YYYY"}</p>
          </div>

          {/* Download Button BELOW certificate */}
          <button className="download-btn" onClick={downloadImage}>
            Download Certificate
          </button>
        </div>

      </div>

    </div>
  );
}