```verilog
module half_adder (input wire a,b,
                   output wire s,c);
  assign s = a ^ b;
  assign c = a & b;
  
endmodule

module full_adder (input wire a,b,cin,
                   output wire s,c);
  wire [2:0] w;
  
  half_adder ha0 (.a(a) , .b(b) , .s(w[0]) , .c(w[1]));
  half_adder ha1 (.a(w[0]) , .b(cin) , .s(s) , .c(w[2]));
  
  assign c = w[1] | w[2] ;
  
endmodule

module array_multiplier ( input wire [3:0] a , b ,
                         output wire [7:0] z );
  
  wire p[0:3][0:3];
  wire [5:0] s ; 
  wire [10:0] c ;
  
  genvar j,k;
  
  generate
  for(j=0; j<4; j=j+1) begin
    for(k=0; k<4; k=k+1) begin
      assign p[j][k]= a[j] & b[k];
    end
  end
  endgenerate
  
  assign z[0] = p[0][0];
  
  
  // row 1
  half_adder h0 (p[1][0] ,p[0][1] ,z[1] ,c[0]);
  half_adder h1 (p[2][0] ,p[1][1] ,s[0] ,c[1]);
  half_adder h2 (p[3][0] ,p[2][1] ,s[1] ,c[2]);
  
  //row 2
  full_adder f0 (p[0][2] ,s[0] ,c[0] ,z[2] ,c[3]);
  full_adder f1 (p[1][2] ,s[1] ,c[1] ,s[2] ,c[4]);
  full_adder f2 (p[2][2] ,p[3][1] ,c[2] ,s[3] ,c[5]);
  
  //row 3
  full_adder f3 (p[0][3] ,s[2] ,c[3] ,z[3] ,c[6]);
  full_adder f4 (p[1][3] ,s[3] ,c[4] ,s[4] ,c[7]);
  full_adder f5 (p[2][3] ,p[3][2] ,c[5] ,s[5] ,c[8]);
  
  //row 4
  half_adder h3 (c[6] ,s[4] ,z[4] ,c[9]);
  full_adder f6 (c[9] ,s[5] ,c[7] ,z[5] ,c[10]);
  full_adder f7 (p[3][3] ,c[10] ,c[8] ,z[6] ,z[7]);
  
endmodule
  
    
