# march-work
Codes of work during march


#### code 1

.home-container {
  padding: 24px;
  max-width: 1200px;
  margin: 0 auto;
}

.subtitle {
  display: flex;
  justify-content: center;
  margin-bottom: 32px;
  
  h2 {
    font-family: Santander Headline, sans-serif;
    font-weight: 700;
    font-size: 28px;
    line-height: 36px;
    color: #000000;
  }
}

.items-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 24px;
}

.item {
  background-color: #ffffff;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s, box-shadow 0.2s;
  cursor: pointer;
  
  &:hover {
    transform: translateY(-4px);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
  }
  
  h3 {
    font-family: Santander Headline, sans-serif;
    font-weight: 600;
    font-size: 18px;
    line-height: 24px;
    color: #ec0000;
    margin-bottom: 12px;
  }
  
  p {
    font-family: Santander Text, sans-serif;
    font-weight: 400;
    font-size: 14px;
    line-height: 20px;
    color: #666666;
  }
}

// Responsive adjustments
@media (max-width: 768px) {
  .items-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  .items-grid {
    grid-template-columns: 1fr;
  }
}
