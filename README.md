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



#### Code 2

<div class="home-container">
  <div class="subtitle">
    <h2>Central de Ajuda</h2>
  </div>
  
  <div class="items-grid">
    <div class="item">
      <h3>Cartões</h3>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam in dui mauris.</p>
    </div>
    
    <div class="item">
      <h3>Empréstimos</h3>
      <p>Fusce suscipit varius mi. Cum sociis natoque penatibus et magnis dis.</p>
    </div>
    
    <div class="item">
      <h3>Investimentos</h3>
      <p>Vestibulum auctor dapibus neque. Proin quam nisl, tincidunt et.</p>
    </div>
    
    <div class="item">
      <h3>Seguros</h3>
      <p>Nulla consequat massa quis enim. Donec pede justo, fringilla vel.</p>
    </div>
    
    <div class="item">
      <h3>Pagamentos</h3>
      <p>Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes.</p>
    </div>
    
    <div class="item">
      <h3>Conta Corrente</h3>
      <p>Nullam quis ante. Etiam sit amet orci eget eros faucibus tincidunt.</p>
    </div>
    
    <div class="item">
      <h3>Atendimento</h3>
      <p>Duis leo. Sed fringilla mauris sit amet nibh. Donec sodales sagittis magna.</p>
    </div>
    
    <div class="item">
      <h3>Poupança</h3>
      <p>Sed consequat, leo eget bibendum sodales, augue velit cursus nunc.</p>
    </div>
  </div>
</div>
